# FF4J notes:

## about feature toggles
From: 
https://martinfowler.com/articles/feature-toggles.html


- Feature toggles can be categorized across two major dimensions: how long the feature toggle will live and how dynamic the toggling decision must be.
  - Release Toggles: Release Toggles allow incomplete and un-tested codepaths to be shipped to production as latent code which may never be turned on. Product Managers may have other reasons for not wanting to expose features even if they are fully implemented and tested. Feature release might be being coordinated with a marketing campaign, for example. Using Release Toggles in this way is the most common way to implement the Continuous Delivery principle of "separating [feature] release from [code] deployment.
    - Short lived (few days/weeks)
    - Effect is very static in nature as requests from all users experience same flags. Usually set at the time of deployment (not release). 
  - Experiment Toggles: Experiment Toggles are used to perform multivariate or A/B testing. Each user of the system is placed into a cohort and at runtime the Toggle Router will consistently send a given user down one codepath or the other, based upon which cohort they are in. By tracking the aggregate behavior of different cohorts we can compare the effect of different codepaths. This technique is commonly used to make data-driven optimizations to things such as the purchase flow of an ecommerce system
    - lives long enough to generate enough data (few Hours to weeks)
    - Effect is very dynamic as request from each user takes different path based on flags.
  - Ops toggles: These flags are used to control operational aspects of our system's behavior. We might introduce an Ops Toggle when rolling out a new feature which has unclear performance implications so that system operators can disable or degrade that feature quickly in production if needed. `kill switches` can be long lived which will allow support teams to disable few heavy features in case of heavy traffic.
  - Permissioning Toggles: These flags are used to change the features or product experience that certain users receive. For example we may have a set of "premium" features which we only toggle on for our paying customers. Or perhaps we have a set of "alpha" features which are only available to internal users and another set of "beta" features which are only available to internal users plus beta users.
    - can be very long lived ( multi-year) in cases where we are controlling premium features for paid customers
    - effect is very dynamic as each user request may be treated differently
 
- Manage different toggles differently:
  - These differences should be embraced, and different toggles managed in different ways, even if all the various toggles might be controlled using the same technical machinery. Initially we might have placed that section behind a Release Toggle while it was under development. We might then have moved it to being behind an Experiment Toggle to validate that it was helping drive revenue. Finally we might move it behind an Ops Toggle so that we can turn it off when we're under extreme load. If we've followed the earlier advice around de-coupling decision logic from Toggle Points then these differences in toggle category should have had no impact on the Toggle Point code at all. However from a feature flag management perspective these transitions absolutely should have an impact. As part of transitioning from Release Toggle to an Experiment Toggle the way the toggle is configured will change, and likely move to a different area - perhaps into an Admin UI rather than a yaml file in source control. Product folks will likely now manage the configuration rather than developers. Likewise, the transition from Experiment Toggle to Ops Toggle will mean another change in how the toggle is configured, where that configuration lives, and who manages the configuration.

Other good links:
- https://dzone.com/articles/feature-toggles-are-one-worst
- https://www.abhishek-tiwari.com/decoupling-deployment-and-release-feature-toggles/

## about ff4j

### features

- **feature store**: For distributed architecture, `feature store` works as central repo for all feature toggles which all the microservices can refer.
- **permission based feature toggles**: 
- **conditional feature toggles**:


- FF4J works using strategies.You can create your own strategies too.

### code and design

- two main classes `WebAPIController` and `*Provider`
  - `provider` has single overridden method `getFF4j` which provides `FF4J` object.
    - `FF4J` object has *xml* where features details are given, datasource connection details, propertystore, featurestore and eventstore instances with datasource given as argument.
  - `WebAPIController` has single method `getWebApiConfiguration` that returns `apiconfig` object. This method takes creates a provider and gets `FF4J` object and gives it to instance of `ApiConfig` class. It also sets various properties of `ApiConfig` like audit, port, authentication and authorization etc
    - 

### trying out jdbc sample

- sample we are trying out is `https://github.com/ff4j/ff4j-samples/tree/master/webapp-jetty/ff4j-sample-simplejdbc`
- Notable changes:
  - change the Jersey class name in `web.xml` 
    - from ` <servlet-class>com.sun.jersey.spi.container.servlet.ServletContainer</servlet-class>` to `<servlet-class>org.glassfish.jersey.servlet.ServletContainer</servlet-class>`
    - got error `UnsatisfiedLinkError: Can't load library: /usr/lib/jvm/java-11-openjdk-amd64/lib/libawt_xawt.so` : 
      - this was resolved when I set JAVA_HOME to amazon corretto instead of `/usr/lib/jvm/java-11-openjdk-amd64`



### API:
- http://localhost:8080/api/ff4j/store
- http://localhost:8080/api/ff4j/store/features/feature_X
- http://localhost:8080/api/ff4j/store/features/feature_X/disable (you need to use post: `curl -X POST --trace-ascii ./temp/debugdump.txt http://localhost:8080/api/ff4j/store/features/feature_X/enable`
- 

### IMP links
- Javadocs: https://javadoc.io/doc/org.ff4j/ff4j-core/latest/org/ff4j/core/package-summary.html
- couchbase support PR: https://github.com/ff4j/ff4j/issues/265
