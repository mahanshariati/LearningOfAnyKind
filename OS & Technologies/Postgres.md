# PostgreSQL – Storage, Indexing, and Transactions

- [PostgreSQL – Storage, Indexing, and Transactions](#postgresql--storage-indexing-and-transactions)
  - [various features found in PostgreSQL](#various-features-found-in-postgresql)
  - [Reconnecting your application after a Postgres failover](#reconnecting-your-application-after-a-postgres-failover)
  - [client handling](#client-handling)



PostgreSQL is a powerful, open source object-relational database system that uses and extends the SQL language combined with many features that safely store and scale the most complicated data workloads. <br>
PostgreSQL has earned a strong reputation for its proven architecture, reliability, data integrity, robust feature set, extensibility, and the dedication of the open source community behind the software to consistently deliver performant and innovative solutions.

## various features found in PostgreSQL

- Data Types
    - Primitives: Integer, Numeric, String, Boolean
    - Structured: Date/Time, Array, Range / Multirange, UUID
    - Document: JSON/JSONB, XML, Key-value (Hstore)
    - Geometry: Point, Line, Circle, Polygon
    - Customizations: Composite, Custom Types
- Data Integrity
    - UNIQUE, NOT NULL
    - Primary Keys
    - Foreign Keys
    - Exclusion Constraints
    - Explicit Locks, Advisory Locks
-Concurrency, Performance
    - Indexing: B-tree, Multicolumn, Expressions, Partial
    - Advanced Indexing: GiST, SP-Gist, KNN Gist, GIN, BRIN, Covering indexes, Bloom filters
    - Sophisticated query planner / optimizer, index-only scans, multicolumn statistics
    - Transactions, Nested Transactions (via savepoints)
    - Multi-Version concurrency Control (MVCC)
    - Parallelization of read queries and building B-tree indexes
    - Table partitioning
    - All transaction isolation levels defined in the SQL standard, including Serializable
    - Just-in-time (JIT) compilation of expressions
    - Asynchronous I/O (AIO)
- Reliability, Disaster Recovery
    - Write-ahead Logging (WAL)
    - Replication: Asynchronous, Synchronous, Logical
    - Point-in-time-recovery (PITR), active standbys
    - Tablespaces
- Security
    - Authentication: GSSAPI, SSPI, LDAP, SCRAM-SHA-256, Certificate, OAuth 2.0, and more
    - Robust access-control system
    - Column and row-level security
    - Multi-factor authentication with certificates and an additional method
- Extensibility
    - Stored functions and procedures
    - Procedural Languages: PL/pgSQL, Perl, Python, and Tcl. There are other languages available through extensions, e.g. Java, JavaScript (V8), R, Lua, and Rust
    - SQL/JSON constructors, query functions, path expressions, and JSON_TABLE
    - Foreign data wrappers: connect to other databases or streams with a standard SQL interface
    - Customizable storage interface for tables
    - Many extensions that provide additional functionality, including PostGIS
- Internationalisation, Text Search
    - Support for international character sets, e.g. through ICU collations
    - Case-insensitive and accent-insensitive collations
    - Full-text search


There are many more features that you can discover in the PostgreSQL [documentation](https://www.postgresql.org/docs/).


## Reconnecting your application after a Postgres failover

When those of us who work on Postgres High Availability explain how HA in Postgres works, we often focus on the server side of the stack. Having a Postgres service running with the expected data set is all-important and required for HA, of course. <br>
In this section, you will learn what happens to your application code and connections when a Postgres failover is orchestrated.<br>
The most important thing to know about client-side HA is that when a failover happens, the connections to Postgres are lost. Your application will get an error when trying to use the previously established connection, without any way to anticipate the situation.<br>
At any point in time after your application has obtained a connection to the Postgres instance, the connection might be lost. The Postgres instance could get lost because of changes in the firewall rules, because of a network equipment failure, because of an ethernet or fiber cable being damaged, and many other reasons. When a failover happens, all currently established connections to the Postgres database service are lost. Your goal is to react to a hardware or software fault in production in the least impacting way for your end users.

## client handling

the client for postgres db using a pgdriver connector:

```Go
func New(c *config.PostgresConfig) (*bun.DB, error) {
	sqldb := sql.OpenDB(pgdriver.NewConnector(
		pgdriver.WithAddr(c.Addr),
		pgdriver.WithUser(c.Username),
		pgdriver.WithPassword(c.Password),
		pgdriver.WithDatabase(c.Database),
		pgdriver.WithInsecure(true),
		pgdriver.WithWriteTimeout(c.WriteTimeout),
		pgdriver.WithReadTimeout(c.ReadTimeout),
		pgdriver.WithDialTimeout(c.DialTimeout),
	))
	sqldb.SetMaxOpenConns(c.MaxOpenConnections)       // Maximum open connections
	sqldb.SetMaxIdleConns(c.MaxIdleConnections)       // Maximum idle connections
	sqldb.SetConnMaxLifetime(c.ConnectionMaxLifeTime) // Connection lifetime
	sqldb.SetConnMaxIdleTime(c.ConnectionMaxIdleTime) // Idle connection timeout
	return cl, nil
}
```

for errors in querying your postgres client you should ignore the postgres transient error (those errors that the client handles itself).
For example you can write a func named IsTransientPostgresError and use that when retrying on broken connections:
```Go
func IsTransientPostgresError(err error) bool {
	if err == nil {
		return false
	}
	// context timeouts are transient
	if errors.Is(err, context.DeadlineExceeded) {
		return true
	}
	// no rows error is not transient
	if errors.Is(err, sql.ErrNoRows) {
		return false
	}

	// transient network / driver errors
	msg := err.Error()
	return strings.Contains(msg, "connection refused") ||
		strings.Contains(msg, "connection reset") ||
		strings.Contains(msg, "broken pipe") ||
		strings.Contains(msg, "EOF") ||
		strings.Contains(msg, "timeout") ||
		strings.Contains(msg, "bad connection")
}
```

examle retry func:

```Go
func Retry(
	ctx context.Context,
	attempts int,
	backoff time.Duration,
	fn func() error,
) error {
	var err error

	for i := 0; i < attempts; i++ {
		if ctx.Err() != nil {
			return ctx.Err()
		}

		err = fn()
		if err == nil {
			return nil
		}

		if !IsTransientPostgresError(err) {
			return err
		}
        
		time.Sleep(backoff)
		backoff *= 2 // exponential backoff
	}

	return err
}
```

