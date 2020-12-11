This sample demonstrates the stack trace I get when trying to use the Structure101 Gradle Plugin.

To reproduce, do the following:

```bash
git clone https://github.com/jzheaux/using-structure101-sonar-plugin.git
cd using-structure101-sonar-plugin
cp $LICENSE .
docker run -d -p 9000:9000 jzheaux/sonar-and-structure101:latest
# wait for sonar to finish starting up
```

where `$LICENSE` is the location of an active Structure101 license file.

At this point, Sonarqube needs to be configured according to the [Structure101 Guide](https://structure101.com/help/java/studio/#sonar/sonarqube-setup.html?TocPath=Build%2520Integration%257CSonarQube%257C_____1).
With that completed, you can run:

```bash
./gradlew clean build sonarqube
```

This task will run the Structure101 Build command using the [configuration in the project](s101/config.xml).
It leverages a Docker image that contains [the Structure101 Build install](https://hub.docker.com/repository/docker/jzheaux/structure101-build).

Once this completes, Sonarqube will show the tangle metrics, but will not specify which files the tangles are in.
These files are listed in `key-measures.xml`, so I think I've still got some configuration incorrect somewhere.
