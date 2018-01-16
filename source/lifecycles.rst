ScaleIT Lifecycle Section
=========================

The lifecycles of different aspects of the ScaleIT ecosystem are presented in this chapter.

From Idea to App
----------------

App Store Lifecycle
--------------------

* Review Process
* etc.

Deploy Lifecycle
----------------

also look into googling: circle ci lifecycle

The stages through which an App goes until it reaches 

* The pull request runs tests and is marked as good to merge into master
* The engineer merges the PR and tests are again run against master
* That commit of master deploys to our centralized staging server
* Sanity checks run automatically on the staging server
* That commit then deploys to production
* Sanity checks run on production
* Success and failure notifications are sent via Slack at every step
* Rollback possible for several weeks (depending on the storage settings)


.. warning::
    Don't forget to create release notes and bump the necessary versions.

    In the event of a rollback, an engineer must manually deploy from their machine to cause the latest release status to change and implicitly “re-activate” continuous deployment.

    There should be checks with kill switches along the way (e.g. for every environment and one final manual approval from shop floor process owners).

    Important people (on call) should get notified of deployments statuses