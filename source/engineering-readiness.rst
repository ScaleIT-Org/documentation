App Behaviour
-------------

|checkbox| Logging

|checkbox| Graceful degradation


Software Engineering
--------------------

|checkbox| Reactive Design \(App Richtlinien\)

|checkbox| [https://projects.teco.edu/projects/scaleit-ap2/wiki/Richtlinien\_App-Entwicklung](
https://projects.teco.edu/projects/scaleit-ap2/wiki/Richtlinien_App-Entwicklung)

Development Process
-------------------

|checkbox| Automated build pipeline


|checkbox| Continuous Integration


|checkbox| Use Dynamic Port ranges 49,152 through 65,535.



.. |checkbox| image:: img/icon_checkbox.png
            :scale: 20%

Maintenance
-------------
* Verification scripts for data base format upgrades
*

Testing
-----------
* CI compatibility
* Container level test suite
* 
* BDD Testing

Production Readiness Checklist 
------------------------------

The Production Readiness Checklist and Microservice Evaluation is an advanced list for ensuring the microservices have a level of production readiness comparable to those of companies such as Uber, Netflix, Google etc [#production_readiness]_.

A. Production-Readiness Checklist
++++++++++++++++++++++++++++++++++++

Production-Ready Service is ...

* Stable and Reliable
* Scalable and Performant
* Fault Tolerant and Prepared for Any Catastrophe
* Properly Monitored
* Documented and Understood

B. Evaluate Your Microservice
++++++++++++++++++++++++++++++++++++


* Stability and Reliability

  - The Development Cycle
  - The Deployment Pipeline
  - Dependencies
  - Routing and Discovery
  - Deprecation and Decommissioning

* Scalability and Performance

  - Knowing the Growth Scale
  - Efficient Use of Resources
  - Resource Awareness
  - Capacity Planning
  - Dependency Scaling
  - Traffic Management
  - Task Handling and Processing
  - Scalable Data Storage

* Fault Tolerance and Catastrophe-Preparedness

  - Avoiding Single Points of Failure
  - Catastrophes and Failure Scenarios
  - Resiliency Testing
  - Failure Detection and Remediation
  - Monitoring
  - Key Metrics
  - Logging
  - Dashboards
  - Alerting
  - On-Call Rotations

* Documentation and Understanding

  - Microservice Documentation
  - Microservice Understanding

.. [#production_readiness] Susan J. Fowler Production-Ready Microservices, https://www.safaribooksonline.com/library/view/production-ready-microservices/9781491965962/