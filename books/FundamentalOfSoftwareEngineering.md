# Fundamental Of Software Engineering - Mark Richard & Neal Ford

`Architecture is about the important stuff…whatever that is.` - Ralph Johnson <br>

## Introduction 

Some architects refer to software architecture as the blueprint of the system, while others define it as the roadmap for developing a system. <br>

The **architecture characteristics** define the success criteria of a system, which is generally orthogonal to the functionality of the system. <br>

**Architecture decisions** define the rules for how a system should be constructed. If a particular architecture decision cannot be implemented in one part of the system due to some condition or other constraint, that decision (or rule) can be broken through something called a variance. <br>

The last factor in the definition of architecture is **design principles**. A design principle differs from an architecture decision in that a design principle is a guideline rather than a hard-and-fast rule. <br><br>

There are eight core expectations placed on a software architect, irrespective of any given role, title, or job description:
- Make architecture decisions
- Continually analyze the architecture
- Keep current with latest trends
- Ensure compliance with decisions
- Diverse exposure and experience
- Have business domain knowledge
- Possess interpersonal skills
- Understand and navigate politics

<br>

#### Make architecture decisions
An architect is expected to **define the architecture decisions and design principles** used to **guide** technology decisions within the team, the department, or across the enterprise. Guide is the key operative word in this first expectation. An architect should guide rather than specify technology choices. The **key** to making effective architectural decisions is asking whether the architecture decision is helping to guide teams in making the right technical choice or whether the architecture decision makes the technical choice for themselves. 

#### Continually analyze the architecture
An architect is expected to continually analyze the architecture and current technology environment and then recommend solutions for improvement. This expectation of an architect refers to architecture vitality, which assesses how viable the architecture that was defined three or more years ago is today, given changes in both business and technology. 

#### Keep current with latest trends
An architect is expected to keep current with the latest technology and industry trends. Developers must keep up to date on the latest technologies they use on a daily basis to remain relevant. 

#### Ensure compliance with decisions
An architect is expected to ensure compliance with architecture decisions and design principles. Ensuring compliance means that the architect is continually verifying that development teams are following the architecture decisions and design principles defined, documented, and communicated by the architect.



#### Diverse exposure and experience
An architect is expected to have exposure to multiple and diverse technologies, frameworks, platforms, and environments. This expectation does not mean an architect must be an expert in every framework, platform, and language, but rather that an architect must at least be familiar with a variety of technologies. An effective software architect should be aggressive in seeking out opportunities to gain experience in multiple languages, platforms, and technologies. A good way of mastering this expectation is to focus on technical breadth rather than technical depth. Technical breadth includes the stuff you know about, but not at a detailed level, combined with the stuff you know a lot about. 



#### Have business domain knowledge
An architect is expected to have a certain level of business domain expertise. 

#### Possess interpersonal skills
An architect is expected to possess exceptional interpersonal skills, including teamwork, facilitation, and leadership. 


#### Understand and navigate politics
An architect is expected to understand the political climate of the enterprise and be able to navigate the politics. <br><br>

### Intersection of software architecture and ...
The following sections delve into some of the newer intersections between the role of architect and other parts of an organization, highlighting new capabilities and responsibilities for architects. <br>
#### Engineering practices
Focusing on engineering practices is important. First, software development lacks many of the features of more mature engineering disciplines. Second, one of the Achilles heels of software development is estimation—how much time, how many resources, how much money? Part of this difficulty lies with antiquated accounting practices that cannot accommodate the exploratory nature of software development, but another part is because we’re traditionally bad at estimation, at least in part because of unknown unknowns. <br> Building Evolutionary Architectures co-opts this idea to create architectural fitness
functions: an objective integrity assessment of some architectural characteristic(s). This assessment may include a variety of mechanisms, such as metrics, unit tests, monitors, and chaos engineering. For example, an architect may identify page load time as an importance characteristic of the architecture. To allow the system to change without degrading performance, the architecture builds a fitness function as a test that measures page load time for each page and then runs the test as part of the continuous integration for the project.

#### Operations/DevOps
The builders of the microservices style of architecture realized that these operational concerns are better handled by operations. By creating a liaison between architecture and operations, the architects can simplify the design and rely on operations for the things they handle best.

#### Process
the way that you build software (process) has little impact on the software architecture (structure).

#### Data
A large percentage of serious application development includes external data storage, often in the form of a relational (or, increasingly, NoSQL) database. Code and data have a symbiotic relationship: **one isn’t useful without the other.**

### Laws of Software Architecture
- Everything in software architecture is a trade-off.
  - If an architect thinks they have discovered something that isn’t a trade-off, more likely they just haven’t identified the trade-off yet.
- Why is more important than how.

<br><br><br><br><br>