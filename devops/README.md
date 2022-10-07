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
