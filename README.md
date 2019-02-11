# nexus

Build a Docker Image for Sonatype Nexus Repository Manager OSS based on an Alpine Base Image

Build the image:
```
$ docker build -t nexus .
```

To run:
```
$ docker run -d -p 8081:8081 --name nexus murican/nexus
```

To test:
```
$ curl -u admin:admin123 http://localhost:8081/service/metrics/ping
```


## Notes

* Default credentials are: `admin` / `admin123` ***CHANGE PASS***

* It can take some time (2-3 minutes) for the service to launch in a
new container.  You can tail the log to determine once Nexus is ready:

```
$ docker logs -f nexus
```

* Installation of Nexus is to `/opt/sonatype/nexus`.  

* A persistent directory, `/nexus-data`, is used for configuration,
logs, and storage. This directory needs to be writable by the Nexus
process, which runs as UID 200.

* Three environment variables can be used to control the JVM arguments

  * `JAVA_MAX_MEM`, passed as -Xmx.  Defaults to `1200m`.

  * `JAVA_MIN_MEM`, passed as -Xms.  Defaults to `1200m`.

  * `EXTRA_JAVA_OPTS`.  Additional options can be passed to the JVM via
  this variable.

  These can be used supplied at runtime to control the JVM:

  ```
  $ docker run -d -p 8081:8081 --name nexus -e JAVA_MAX_HEAP=768m murican/nexus
  ```
