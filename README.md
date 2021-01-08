#Stormpath is Joining Okta
We are incredibly excited to announce that [Stormpath is joining forces with Okta](https://stormpath.com/blog/stormpaths-new-path?utm_source=github&utm_medium=readme&utm-campaign=okta-announcement). Please visit [the Migration FAQs](https://stormpath.com/oktaplusstormpath?utm_source=github&utm_medium=readme&utm-campaign=okta-announcement) for a detailed look at what this means for Stormpath users.

We're available to answer all questions at [support@stormpath.com](mailto:support@stormpath.com).

# WAR files with Spring Boot

This is the code developed in the tutorial on deploying Spring Boot apps as a WAR.

It modifies an existing simple REST app https://github.com/stormpath/stormpath-spring-boot-jpa-example

### Requirements

- Maven
- JDK 7
- Tomcat 7

### Running

To build and start the server simply type

```sh
$ mvn spring-boot:run
```

from the root directory.

### Deploying on Tomcat

First build the WAR with

```sh
$ mvn clean package
```

Then copy the output WAR to Tomcat's webapps directory.

On Ubuntu the command is

```sh
$ sudo cp target/demo-0.0.1-SNAPSHOT.war /var/lib/tomcat7/webapps/demo.war
```


### Using

You can see what urls are available using curl:

```sh
$ curl localhost:8080/demo
```

You can view existing people objects using a similar request:

```sh
$ curl localhost:8080/demo/persons
```

and can create new ones using a POST:

```sh
$ curl -X POST -H "Content-Type:application/json" -d '{ "firstName" : "Karl", "lastName" : "Penzhorn" }' localhost:8080/demo/persons
```

### Todo

 - Different build profiles

### License
----

MIT
