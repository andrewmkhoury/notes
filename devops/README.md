# What is devops?
DevOps integrates the development and operations team by implementing automation of infrastructure, workflows, building and deploying code, etc. in order to improve collaboration and productivity.  Code is built and deployed in small pieces.  All development is test-driven and application performance is continuously being measured.

* Reduce org. silos
* Accept failure
* Implement changes gradually
* Use tooling and automation vs. manual work
* Measure everything

## VMs vs. Containers
* VMs each have an OS and containers share the host OS
* Containers
  * Similar to VMs, but more lightweight
  * Relaxed isolation properties to share the OS between apps.
  * Container has its own filesystem, share of CPU, memory, process space, and more.
  * Decoupled from the underlying infrastructure - this makes them portable across clouds and OS distros.

## Container Orchestration
Container orchestration automates the deployment, management, scaling, and networking of containers. Enterprises that need to deploy and manage hundreds or thousands of Linux® containers and hosts can benefit from container orchestration. 

Container orchestration tools provide a framework for managing containers and microservices architecture at scale. There are many container orchestration tools that can be used for container lifecycle management. Some popular options are Kubernetes, Docker Swarm, and Apache Mesos.

https://www.redhat.com/en/topics/containers/what-is-container-orchestration

## Site Reliability Engineering
### Intro
*What is it?*
* It is a job title / role
* It applies Software Eng. principles to Infra and Ops.
* Uses automation to provide service at scale.
* Companies put a cap on Ops work vs. Dev work - usually 50/50 time split.
* DevOps vs SRE - DevOps is a philosophy. SRE can be viewed as an applied implementation of DevOps concepts.

*Tenets of SRE:*
Durable focus on engineering
  * Monitor % of Ops work
  * Product Dev after 50% Ops

Innovation vs. Stability
* Error budget of 0.01% if reliability target is 99.99%
* Determine reliability target:
  * What can users tolerate?
  * What is the user experience?
* Spend error budget taking risks launching some things quickly

Monitoring
* Alerts
* Tickets
* Logging

Emergency Response
* Reliability - Mean time to failure vs. mean time to restore service
* System w/ more failures but less human intervention is usually more reliable
* Practiced Engineer + Playbook (aka Runbook)

Change Management
* Progressive rollouts
* Quickly and accurately detect problems
* Rolling back changes safely

Provisioning
* Provisioning = Change management + Capacity Planning
* Provisioning must be fast and only when necessary


### Observability
* 3 Pillars
  * Metrics - Key-value pair metrics for alerts and dashboards
  * Logs - Gather logs in central location for analysis
  * Traces - Tracking transactions between components
  
* Metrics and Monitoring
  * Time series data
  * Automated processing of metrics
  * Build visual dashboards
  * Prometheus and New Relic are metrics platforms
  
* Logging
  * Create code that logs properly
  * After fact analysis
  * Build dashboards, queries, reports
  * Splunk, Elastic Search, & SumoLogic are tools

* Distributed Tracing
  * Tracing microservice / distributed architecture
  * Install agents
  * Gather results to central location
  * Analyze individual traces for performance, capacity and failure
  * Jaeger, Zipkin and New Relic do tracing
  
### Introduction to SLx
* SL = Service Level, x = different factors that can impact your work as SRE
* SLI = Service Level Indicator - Aspect of service being measured - e.g. latency
* SLO = Service Level Objective - Target value for SLI - e.g. 99% of requests < 100ms
* SLA = Service Level Agreement - If SLO is not met - e.g. 10% service credit for latency < 98.5%

#### SLI
Aspect of service being measured *that affects customer service*
* What do the users care about?
  * User-Facing - Availability, Latency, Throughput
  * Storage - Latency, Availability, Durability
  * Big Data - Throughput, End-to-end latency

*Collecting Indicators*
Server-side:
* Gather metrics - e.g. Prometheus
* Analyze logs - e.g. HTTP 500 statuses / total responses

Client-side:
* Page load time

Aggregation of the data
* Averages aren't usually helpful
* Use [percentiles](https://en.wikipedia.org/wiki/Percentile) to see outliers
* Use known good test input data

SLOs/SLTs - Service Level Objectives or Service Level Targets
*What makes an SLO useful?*
* User cares about it
* Don't define an SLO for every SLI

SLO Expectations
* Keep a safety margin
* Don't overachieve
* Understand if you need to make the system faster, more available or more resilient

### SLA
Crafting SLA involves business and legal teams.  Be conservative in what is advertised to users.

Error Budget
* Balance stability of your product with deployment speed
* SLOs should never be 100% - 99.9% is more acceptable = 43 mins / month.

Error Budget Motivation
* Software fault tolerance
* Testing
* Push frequency
* Canary Duration / Size

Forming Error Budget
* Uptime is measured by monitoring system
* If you haven't hit your error budget then you can push a release
* Throttle based on budget

## Toil
### What is toil?
Manual, repetitive and automatable tasks are toil.

* Not related to project tracking, etc.
* Manual labor - ssh'ing into systems, repetitive work, etc.
* Toil is interrupt driven - reacting to PagerDuty alerts is toil.
* It has little to no lasting impact (enduring value).
* Toil tasks could be automated.

### Why is toil bad?
* Toil directly reduces project work.
* Toil promotes attrition.
* Lowers morale.
* Slows career progress when you spend too little time on projects.
* Creates confusion about SRE role.
* Sets a precedent.
* Too much of it can effectively demote an SRE to Ops engineers.

### How to measure toil
* SREs want ample time for long term engineering work.
* But also responsible for Ops work.
* Analyze cost / benefit.  SREs aim for less than 50% time on toil.

Measuring Toil
1. Identify - processes, prod interruptions, migrations, troubleshooting, capacity planning
2. Quantify - effort, time spent on toil, number of toil tickets.
3. Track - Store datapoints, automate measuring, assess efficiency of toil reduction efforts.

Reducing Toil
* Reject - Costs of doing/not doing, delay to do in batches, use SLO/error budget.
* Relay - Promote toil reduction as feature, provide self-service.
* Remove - Eliminate source of toil, automate response.

## Infrastructure as Code
### Automation Tools
Config Management
* Manage software and configs on machines
* e.g. Ansible, puppet, chef, smutje

Server Templating
* Create VMs or Containers
* e.g. Packer, Docker

Orchestration
* Manage fleet of VMs or Containers
* e.g. ECS, Kubernetes

Provisioning
* Create foundational infrastructure
* Terraform, CloudFormation, ARM

### IaC Benefits

Source Code Management
* Archive - keep track of source code
* Audit Log - what changed and when
* Review of Changes - pull requests - this helps w/ finding bugs / knowledge sharing
* e.g. Git / Github

CI/CD
Pull-Requests for code review
* 4 eye principle
* Automation to validate changes and change requests

Automatic Deployment
* CMR integration
* Deployment messages via chat, email, etc.

Automation in General
* Consistent
* Faster
* Repeatable
* Self-Service

## Availability, Maintainability, & Reliability
* Reliability = likelihood of a service functioning correctly in user interaction.
* Availability + Maintainability affects Reliability of a service.
* Reliability is a measure of "customer happiness"
* Cost of improving reliability may exceed benefits

## Availability
* % of time that service is functioning.
* Availability = Uptime/(Uptime + Downtime)
* SRE paradigm teaches us "failure is inevitable" - we never say 100% available or reliable.
See [here](https://sre.google/sre-book/availability-table/) for a chart. 

### Maintainability
* Proactive Maintainability - build codebase that is easy to change and read.
* Reactive Maintainability - ability to repair after incidents.
* Maintainability - reflected in availability metrics.

### Reliability
Likelihood of service working correctly when accessed by user.

Only if the users access the service uniformly across all features all the time does Availability determine Reliability.

### Risk
Cost doesn't increase with reliability.

* Cost of redundant compute resources.
* Cost of opportunity.

An incremental improvement in reliability may cost 100x more than the previous increment.


## SRE Best Practices
* Immutable Infra. - Comparison, Baking process
* Auto-scaling - Vertical vs. Horizontal
* Service Resiliency - Circuit Breaker, rate limiting, retries, time outs, health checks, fallbacks

### Immutable Infra.
If a server needs an update or fix then new server is deployed.  A new version of the architecture is built and deployed to production during changes.

Benefits
* Builds reliability, consistency, and confidence.


Comparison
* Mutable - Low initial cost, but deploying on mutable infra gets complex as changes occur on the same system.  Config drifts are likely.
* Immutable Infra - Deploy what you test, but initial cost is high.

Baking Process
1. Base Image - Baking process starts with base image - Linux or container base.
2. Infra as Code Deploy - Config OS, install software, deploy of service, setup monitoring.
3. Hardening - Disable non-required users, update system components, config firewalls.
4. Publishing - Created image is copied to registry for deployment.

### Auto-scaling
Adjust resources according to usage.

Vertical vs. Horizontal
* Vertical - add CPU, memory, etc. to single node.
* Horizontal - add more compute by adding more server instances.

Metrics to drive scaling:
* CPU Usage
* Network Usage
* Requests per instance
* Message queue length
* Writes & Reads / second

### Service Resiliency
When there is an outage we can still provide some level of service.

Some comonents to help in resiliency
* Health Checking
* Rate Limiting
* Timeouts
* Fallbacks
* Circuit Breaker
* Retries

Health Check
* Load balancer has an endpoint that responds if it is healthy or not or if it doesn't respond then it is considered unhealthy as well.
* Shallow - if service can respond.
* Deep - Check service and its dependencies. ONLY check vital service dependencies such as the database.

Rate Limiting
* Put a cap on repeat actions to avoid overload.
* Prevent user from overloading system.
* Prevent malicious bot activity.
* Reduce strain on servers.

Timeouts
* How long to wait for backend before giving up.
* Incoming requests will block until they receive timeout.
* Connection timeout: time to get a connection established.
* Socket timeout: time to wait for a socket to read data.
* Response, transaction or "timeout": time to wait for overall response to be received.

Fallbacks
* fail over to a different option if one service is down.

Circuit Breaker
* Prevent bigger outages by failing fast.
* See [here](https://medium.com/bonniernewstech/circuit-breaker-pattern-what-and-why-a17f8babbec0)

Retries
* Try request again if it fails.
* When retries make sense - indeterminate failures - Temporary network problem (packet loss), no or slow responses
* Some errors shouldn't be retried - software responds with specific determinate error.

Retries + Exponential Back-off
* Time to delay retry in case of failed requests.
* If retry fails give double time before trying again.
