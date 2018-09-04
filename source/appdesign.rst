.. _app design:
ScaleIT App Design-Prinzipien
=============================

In diesem Kapitel werden Design-Prinzipien vorgestellt die dazu dienen eine saubere Implementierung der Software unterstützen. Diese Entwicklungsprinzipien sind eine Sammlung von Best-Practices aus der modernen Software-Entwicklung und fokussieren sich auf die Bedürfnisse des betrieblichen Hallenbodens.

Eine App ist ein logische Konstrukt, dass der verbesserung der User-Experience (UX) dient.

Die konkrete softwaretechnische Architektur der ScaleIT Plattform wird in Kapitel `ScaleIT Architektur`_ beschrieben.

Die App Compliance Level werden im Kapitel `Compliance Level`_ beschrieben.

App Software-Design-Prinzipien
------------------------------

ScaleIT Apps are a model of the pattern of multiple cooperating processes which form a cohesive unit of service. They simplify application deployment and management by providing a higher-level abstraction than the set of their constituent applications. Apps serve as unit of deployment, horizontal scaling, and replication. Colocation (co-scheduling), shared fate (e.g. termination), coordinated replication, resource sharing, and dependency management should be handled automatically for containers in a app.

The applications in an App all use the same network namespace (same IP and port space), and can thus “find” each other and communicate using localhost. Because of this, applications in an App must coordinate their usage of ports. Each App has an IP address in a flat shared networking space that has full communication with other physical computers and Apps across the network.
(Adapted from Kubernetes Pods).


Leveraging Bounded Contexts
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Zum Zweck der Modularisierung von Software eignet sich das Prinzip des Bounded Context [DDDEvans]_ [FowlerBoundedContext]_.

Bounded Context is a central pattern in Domain-Driven Design1. It is the focus of DDD's strategic design section which is all about dealing with large models and teams. DDD deals with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships.
DDD is about designing software based on models of the underlying domain. As you try to model a larger domain however, it gets progressively harder to build a single unified model. Different groups of people will use subtly different vocabularies in different parts of a large organization. So instead DDD divides up a large system into Bounded Contexts, each of which can have a unified model - essentially a way of structuring the domain into multiple canonical models [FowlerMultipleCanonicalModels]_.

Bounded Contexts use the principle of Shared- and Hidden Models [NewmanMicroservices]_, where each Bounded Context exposes an explicit interface to the outside world, the Shared Model, while the Hidden Models are irrelevant to other Bounded Contexts and therefore kept encapsulated privately.

.. figure:: img/bounded_context_example.png
   :alt: Shared Model showing two bounded contexts

   Shared Model showing two bounded contexts

A Bounded Context is a unit of function with business value, that has high cohesion and reprensents a part of the domain (subdomain) or in other words it is a specific responsibility enforced by explicit boundaries [BoundedContextExplained]_. Examples: Billing, Machine Control Interface


.. todo::
    App Richtlinien aus der Wiki hinzufügen


.. include:: app_interface_design.rst


Bibliography
------------

.. [DDDEvans] E. Evans, Domain-Driven Design: Tackling Complexity in the Heart of Software. Addison-Wesley Professional, 2003.

.. [FowlerMicroservices] J. Lewis and M. Fowler, “Microservices @ Martinfowler.Com,” 2014. [Online]. Available: http://martinfowler.com/articles/microservices.html.

.. [NewmanMicroservices] S. Newman, Building Microservices. O’Reilly Media, 2015.

.. [FowlerBoundedContext] “BoundedContext @ martinfowler.com.” [Online]. Available: http://martinfowler.com/bliki/BoundedContext.html.

.. [FowlerMicroservicePrerequisites] “MicroservicePrerequisites @ martinfowler.com.” [Online]. Available: http://martinfowler.com/bliki/MicroservicePrerequisites.html.

6 “Microservices Resource Guide @ martinfowler.com.” [Online]. Available: http://martinfowler.com/microservices/.

7 C. van den Thillart, G. Vermaas, M. van der Linden, and J. Vermeir, “microservices-principles @ blog.xebia.com.” [Online]. Available: http://blog.
xebia.com/tag/microservices-principles/.

.. [FowlerMultipleCanonicalModels] 8 “MultipleCanonicalModels @ martinfowler.com.” [Online]. Available: http://martinfowler.com/bliki/MultipleCanonicalModels.html.

9 “streamprocessing @ cloud.google.com.” [Online]. Available: https://cloud.google.com/solutions/architecture/streamprocessing.

10 “Unix_philosophy @ en.wikipedia.org.” [Online]. Available: https://en.wikipedia.org/wiki/Unix_philosophy#Eric_Raymond.E2.80.99s_17_Unix_Rules.

11 A. Wiggins, The Twelve-Factor App. 2012.

12 “Software Architecture @ Msdn.Microsoft.Com.” [Online]. Available: https://msdn.microsoft.com/en-us/library/ee658124.aspx.

.. [BoundedContextExplained] “DDD - The Bounded Context Explained.” [Online]. Available: http://blog.sapiensworks.com/post/2012/04/17/DDD-The-Bounded-Context-Explained.aspx.

14 The 6 Traits of Reactive Microservices: Isolated, Asynchronous, Autonomous and more [Online]. Available: https://www.lightbend.com/blog/the-6-traits-of-reactive-microservices-isolated-asynchronous-autonomous

15 Richardson Maturity Model (REST), http://martinfowler.com/articles/richardsonMaturityModel.html

16 Rubber Duck Debugging, https://en.wikipedia.org/wiki/Rubber_duck_debugging

.. [Nielsen10] Jakob Nielsen, Ten Usability Heuristics, January 1, 1995, online: https://www.nngroup.com/articles/ten-usability-heuristics/