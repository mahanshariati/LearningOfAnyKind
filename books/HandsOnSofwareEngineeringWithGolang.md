# Hands-On Software Engineering With Golang - Achilleas Anagnostopoulos
## Overview

## Chapter 13: Metrics Collection and Visualization
Converting monolithic applications into a set of microservices requires monitoring the health of each individual service and being notified when problems arise.

- Prometheus: a popular metrics collection system written entirely in Go.

covered topics:
- Explaining the differences between essential SRE terms such as SLIs, SLOs, and SLAs
- Comparison of push- and pull-based systems for metrics collection and an analysis of the pros and cons of each approach
- Setting up Prometheus and learning how to instrument your Go applications for
collecting and exporting metrics
- Running Grafana as the visualization frontend for our metrics
- Using the Prometheus ecosystem tools to define and handle alerts

### Monitoring from the perspective of a site reliability engineer

monitoring the state and performance of software systems is one of the key responsibilities associated with the role of a site reliability engineer (SRE). <br> <br>
**Service-level indicators (SLIs)**: An SLI is a type of metric that allows us to quantify the perceived quality of a service from the perspective of the end user. <br>
some common types of SLIs:
- Availability
- Throughput
- Latency

**Service-level objectives (SLOs)**: An SLO is defined as the range of values for an SLI that allows us to deliver a particular level of service to an end user or customer. <br>
SLO definitions generally consist of three parts:
- a description of the thing that we are measuring (the SLI)
- the expected service level expressed as a percentage
- the period where the measurement takes place

Service-level agreements (SLAs): An SLA is an implicit or explicit contract between a service provider and one or more
service consumers. The SLA outlines a set of SLOs that have to be met and the
consequences for both meeting and failing to meet them.

### Exploring options for collecting and aggregating metrics
Monitoring and metrics aggregation systems can be classified into two broad categories based on the entity that initiates the data collection:
- In a push-based system, the client (for example, the application or a data collection service running on a node) is responsible for transmitting the metrics data to the metrics aggregation system.
- In a pull-based system, metrics collection is the responsibility of the metrics aggregation system. In an operation commonly referred to as scraping the metrics system initiates a connection to the metrics producers and retrieves the set of available metrics.

In a pull-based system, the ingestion rate for metrics is under the control of the collector. Collectors can react to sudden spikes in metric production rates by adjusting their scrape rates to compensate. Pull-based systems are generally considered to be more scalable than their push-based counterparts. <br>

pull-based metrics system assumes that the collector can always establish a connection to the
various endpoints. However, this may not always be possible! Consider a scenario where
we want to scrape a service that has been deployed to a private subnet. That particular
subnet is pretty much locked down and does not allow ingress traffic from the subnet that
the collector is deployed to. In such a case, our only option would be to use a push-based
mechanism to get the metrics out (while ingress traffic is blocked, egress traffic is typically
allowed). <br>

### The Prometheus architecture
![alt text](images/image.png)

- The **Prometheus server** is the core component of Prometheus. Its primary responsibility is to periodically scrape the configured set of targets and persist any collected metrics into a time-series database. As a secondary task, the server evaluates an operator-defined list of alert rules and emits alert events each time any of those rules are satisfied. 
- The **Alertmanager component** ingests any alerts emitted by the Prometheus server and sends notifications through one or more communication channels (for example, email, Slack, or a third-party pager service).
- The **service discovery layer** enables Prometheus to dynamically update the list of endpoints to scrape.
- The **Pushgateway component** emulates a push-based system for collecting metrics from sources that cannot be scraped.
- Clients retrieve data from Prometheus by submitting queries written in a
bespoke query language referred to as **PromQL**.

### metric types
- **Counters**: A counter is a cumulative metric whose value increases monotonically over time. Counters can be used to track the number of requests to a service, the number of downloads for an application, and so on.
- **Gauges**: A gauge tracks a single value that can go up or down. A common use case for gauges is to record usage (for example, CPU, memory, and load) stats about a server node and metrics such as the total number of users currently connected to a particular service.
- **Histograms**: A histogram samples observations and assigns them to a preconfigured number of buckets.
- **Summaries**: Summaries perform quantile calculations directly on the client and can be used as an alternative for reducing the query load on the server.


### automating the detection of scrape targets
A **static scrape configuration** is considered the canonical way of providing scrape targets to
Prometheus. The operator includes one or more static configuration blocks in the
Prometheus configuration file that define the list of target hosts to be scraped and the set of
labels to apply to the scraped metrics. <br>
```bash
static_configs:
    - targets:
    - "host1"
    - "host2"
labels:
    service: "my-service"
```
An issue with the static config approach is that after updating the Prometheus configuration files, we need to restart Prometheus so it can pick up the changes.
<br>

A better alternative is to **extract the static configuration blocks to an external file** and then reference that file from within the Prometheus configuration. and then reference that file from within the Prometheus configuration via the file_sd_config option:
```bash
file_sd_configs:
    - files:
        - config.yaml
    refresh_interval: "5m"
```
When file-based discovery is enabled, Prometheus will watch the specified set of files for changes and automatically reload their contents once a change has been detected. 


### Instrumenting Go code 
In order for Prometheus to be able to scrape metrics from our deployed services, we need to perform the following sequence of steps:
1. Define the metrics that we are interested in tracking.
2. Instrument our code base so that it updates the values of the aforementioned metrics at the appropriate locations.
3. Collect the metric data and make it available for scraping over HTTP. 

the official Go client package for Prometheus:
```bash
go get github.com/prometheus/client_golang/prometheus
go get github.com/prometheus/client_golang/prometheus/promauto
go get github.com/prometheus/client_golang/prometheus/promhttp
```

**promauto** is a subpackage of the Prometheus client that defines a set of convenience helpers for creating and registering metrics with the minimum possible amount of code. Each of the constructor functions from the promauto package returns a Prometheus metric instance that we can immediately use in our code.

```bash
numReqs := promauto.NewCounter(prometheus.CounterOpts{
    Name: "app_reqs_total",
    Help: "The total number of incoming requests",
})
// Increment the counter.
numReqs.Inc()
// Add a value to the counter.
numReqs.Add(42)
```

Each Prometheus metric must be assigned a unique name. If we attempt to register a metric with the same name twice, we will get an **error**. What's more, when registering a new metric, we can optionally specify a help message that provides additional information about the metric's purpose.<br>

The next type of metric that we will be instantiating is a **gauge**. Gauges are quite similar to counters with the exception that their value can go either up or down.

```bash
queueLen := promauto.NewGauge(prometheus.GaugeOpts{
    Name: "app_queue_len_total",
    Help: "Total number of items in the queue.",
})
// Add items to the queue
queueLen.Inc()
queueLen.Add(42)
// Remove items from the queue
queueLen.Sub(42)
queueLen.Dec()
```

The **NewHistorgram** constructor expects the caller to specify a strictly ascending list of float64 values that describe the width of each bucket that's used by the histogram. <br>

```bash
reqTimes := promauto.NewHistogram(prometheus.HistogramOpts{
    Name: "app_response_times",
    Help: "Distribution of application response times.",
    Buckets: prometheus.LinearBuckets(0, 100, 20),
})
// Record a response time of 100ms
reqTimes.Observe(100)
```

Adding values to a histogram instance is quite trivial. All we need to do is simply invoke its Observe method and pass the value we wish to track as an argument. <br>

One of the more interesting Prometheus features is its support for partitioning collected samples across one or more dimensions (labels, in Prometheus terminology). If we opt to use this feature, instead of having a single metric instance, we can work with a vector of metric values.

```bash
regCountVec := promauto.NewCounterVec(
prometheus.CounterOpts{
    Name: "app_registrations_total",
    Help: "Total number of registrations by A/B test layout.",
},
[]string{"layout"},
)
regCountVec.WithLabelValues("a").Inc()
```

This time, instead of a single counter, we will be creating a vector of counters where every sampled value will be automatically tagged with a label named layout. To increment or add value to this metric, we need to obtain the correct counter by invoking the variadic WithLabelValues method on the regCountVec variable. his method expects a string value for each defined dimension and returns the counter instance that corresponds to the provided label values. <br>

**Exposing metrics for scraping** <br>
After registering our metrics with Prometheus and instrumenting our code to update them where needed, the only additional thing that we need to do is expose the collected values over HTTP so that Prometheus can scrape them. <br> The promhttp subpackage from the Prometheus client package provides a convenience helper function called Handler that returns an http.Handler instance that encapsulates all the required logic for exporting collected metrics in the format expected by Prometheus. <br>
The exported data will not only include the metrics that have been registered by the developer but it will also contain an extensive list of metrics that pertain to the Go runtime. Some examples of such metrics are as follows:
- The number of active goroutines
- Information about stack and heap allocation
- Performance statistics for the Go garbage collector

```bash 
func main() {
    // Create a prometheus counter to keep track of ping requests.
    numPings := promauto.NewCounter(prometheus.CounterOpts{
        Name: "pingapp_pings_total",
        Help: "The total number of incoming ping requests",
    })
    http.Handle("/metrics", promhttp.Handler())
    http.Handle("/ping", http.HandlerFunc(func(w http.ResponseWriter, _
  *http.Request) {
        numPings.Inc()
        w.Write([]byte("pong!\n"))
    }))
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

### Visualizing collected metrics using Grafana
Grafana offers a convenient, end-to-end solution that can be used to retrieve metrics from a variety of different data sources and construct dashboards for visualizingu them. <br>
In terms of supported visualization widgets, the standard Grafana installation supports the following widget types:
- **Graph**: A flexible visualization component that can plot single- and multi-series line charts or bar charts. Furthermore, graph widgets can be configured to display multiple series in overlapping or stacked mode. 
- **Logs panel**: A list of log entries that are obtained by a compatible data source (for example, Elasticsearch) whose contents are correlated with the information displayed by another widget.
- **Singlestat**: A component that condenses a series into a single value by applying an aggregation function (for example, min, max, avg, and so on). This component may optionally be configured to display a sparkline chart or to be rendered as a gauge.
- **Heatmap**: A specialized component that renders the changes in a histogram's set of values over time. As shown in the following screenshot, heatmaps comprise a set of vertical slices where each slice depicts the histogram values at a particular point in time. Contrary to a typical histogram plot, where bar heights represent the count of items in a particular bucket, heatmaps apply a color map to visualize the frequency of items within each vertical slice.
- **Table**: A component that is best suited for rendering series in tabular format.

### Using Prometheus as an end-to-end solution for alerting

