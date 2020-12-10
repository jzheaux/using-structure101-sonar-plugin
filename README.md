This sample demonstrates the stack trace I get when trying to use the Structure101 Gradle Plugin.

To reproduce, do the following:

```
git clone https://github.com/jzheaux/using-structure101-sonar-plugin.git
cd using-structure101-sonar-plugin
cp $LICENSE .
docker run -d -p 9000:9000 jzheaux/sonar-and-structure101:latest
# wait for sonar to finish starting up
java -Ds101.label=1.0.0 -jar ~/tools/structure101/java/structure101-java-build.jar structure101-build-config.xml
./gradlew sonarqube --stacktrace --debug
```

where `$LICENSE` is the location of an active Structure101 license file.
