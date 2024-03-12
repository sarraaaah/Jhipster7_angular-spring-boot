Get Started with JHipster 7.9.4
//
node v20.11.1
java v16.0.2
Angular v17.2.3
npm v10.2.4
mvn v3.2.5


//
- What's Jhipster?
JHipster is a free and open-source application generator used to quickly develop modern web applications and Microservices using Angular or React (JavaScript library) and the Spring Framework.

Overview: JHipster provides tools to generate a project with a Java stack on the server side (using Spring Boot) and a responsive Web front-end on the client side (with Angular/React and Bootstrap). It can also create microservice stack with support for Netflix OSS, Docker and Kubernetes.

The term 'JHipster' comes from 'Java Hipster', as its initial goal was to use all the modern and 'hype' tools available at the time.Today, it has reached a more enterprise goal, with a strong focus on developer productivity, tooling and quality.

Major functionalities:
. Generate full stack applications and microservices, with many options
. Generate CRUD entities, directly or by scaffolding
. Database migrations with Liquibase
. NoSQL databases support (Cassandra, MongoDB, Neo4j)
. Elasticsearch support
. Websockets support
. Automatic deployment to CloudFoundry, Heroku, OpenShift, AWS

Technology stack :

#On the client side:

HTML5 Boilerplate
Twitter Bootstrap
AngularJS
Full internationalization support with Angular Translate
Optional Compass / Sass support for CSS design
Optional WebSocket support with Spring Websocket

#On the server side:

Spring Boot
Spring Security (including Social Logins)
Spring MVC REST + Jackson
Monitoring with Metrics
Optional WebSocket support with Spring Websocket
Spring Data JPA + Bean Validation
Database updates with Liquibase
Elasticsearch support
MongoDB support
Cassandra support
Neo4j support

Out-of-the-box auto-configured tooling:

Yeoman
Webpack or Gulp.js
BrowserSync
Maven or Gradle
Editor for Datamodeling (visual and textual)

OAuth 2.0 / OpenID Connect
an excellent way to secure your JHipster application. If you're not sure what OAuth and OpenID Connect (OIDC) are, please see What the Heck is OAuth?

To log in to your app, you'll need to have Keycloak up and running. The JHipster Team has created a Docker container for you that has the default users and roles. Start Keycloak using the following command.

docker-compose -f src/main/docker/keycloak.yml up
The security settings in src/main/resources/application.yml are configured for this image.

security:
    basic:
        enabled: false
    oauth2:
        client:
            accessTokenUri: http://localhost:9080/auth/realms/jhipster/protocol/openid-connect/token
            userAuthorizationUri: http://localhost:9080/auth/realms/jhipster/protocol/openid-connect/auth
            clientId: web_app
            clientSecret: web_app
            clientAuthenticationScheme: form
            scope: openid profile email
        resource:
            userInfoUri: http://localhost:9080/auth/realms/jhipster/protocol/openid-connect/userinfo
            tokenInfoUri: http://localhost:9080/auth/realms/jhipster/protocol/openid-connect/token/introspect
            preferTokenInfo: false
Okta
If you'd like to use Okta instead of Keycloak, you'll need to change a few things. First, you'll need to create a free developer account at https://developer.okta.com/signup/. After doing so, you'll get your own Okta domain, that has a name like https://dev-123456.oktapreview.com.

Modify src/main/resources/application.yml to use your Okta settings.

security:
    basic:
        enabled: false
    oauth2:
        client:
            accessTokenUri: https://{yourOktaDomain}.com/oauth2/default/v1/token
            userAuthorizationUri: https://{yourOktaDomain}.com/oauth2/default/v1/authorize
            clientId: {clientId}
            clientSecret: {clientSecret}
            clientAuthenticationScheme: form
            scope: openid profile email
        resource:
            userInfoUri: https://{yourOktaDomain}.com/oauth2/default/v1/userinfo
            tokenInfoUri: https://{yourOktaDomain}.com/oauth2/default/v1/introspect
            preferTokenInfo: false
Create an OIDC App in Okta to get a {clientId} and {clientSecret}. To do this, log in to your Okta Developer account and navigate to Applications > Add Application. Click Web and click the Next button. Give the app a name you’ll remember, specify "http://localhost:8080" as a Base URI, and "http://localhost:8080/login" as a Login Redirect URI. Click Done and copy the client ID and secret into your application.yml file.

Navigate to API > Authorization Servers, click the Authorization Servers tab and edit the default one. Click the Claims tab and Add Claim. Name it "groups" or "roles", and include it in the ID Token. Set the value type to "Groups" and set the filter to be a Regex of .*.

After making these changes, you should be good to go! If you have any issues, please post them to Stack Overflow. Make sure to tag your question with "jhipster" and "okta".
