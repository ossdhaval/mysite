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
    - 

## about ff4j

- **feature store**: For distributed architecture, `feature store` works as central repo for all feature toggles which all the microservices can refer.
- **permission based feature toggles**: 
- **conditional feature toggles**:


- FF4J works using strategies.You can create your own strategies too.


## trying out jdbc sample

- sample we are trying out is `https://github.com/ff4j/ff4j-samples/tree/master/webapp-jetty/ff4j-sample-simplejdbc`
- Notable changes:
  - change the Jersey class name in `web.xml` 
    - from ` <servlet-class>com.sun.jersey.spi.container.servlet.ServletContainer</servlet-class>` to `<servlet-class>org.glassfish.jersey.servlet.ServletContainer</servlet-class>`
    - got error `UnsatisfiedLinkError: Can't load library: /usr/lib/jvm/java-11-openjdk-amd64/lib/libawt_xawt.so` : 
      - this was resolved when I set JAVA_HOME to amazon corretto instead of `/usr/lib/jvm/java-11-openjdk-amd64`



## API:
- http://localhost:8080/api/ff4j/store
- http://localhost:8080/api/ff4j/store/features/feature_X
- http://localhost:8080/api/ff4j/store/features/feature_X/disable (you need to use post: `curl -X POST --trace-ascii ./temp/debugdump.txt http://localhost:8080/api/ff4j/store/features/feature_X/enable`
- 
