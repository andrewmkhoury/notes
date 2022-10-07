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


