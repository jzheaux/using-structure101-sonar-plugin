This sample demonstrates the stack trace I get when trying to use the Structure101 Gradle Plugin.

To reproduce, do the following:

```
git clone https://github.com/jzheaux/using-structure101-sonar-plugin.git
cd using-structure101-sonar-plugin
cp $LICENSE .
docker run -d -p 9000:9000 jzheaux/sonar-and-structure101:latest
# wait for sonar to finish starting up
./gradlew sonarqube -Dstructure101.reportdir=`pwd` --stacktrace --debug
```

where `$LICENSE` is the location of an active Structure101 license file.

The exception is:

```bash
13:24:24.026 [DEBUG] [com.sun.xml.internal.bind.v2.runtime.reflect.opt.Injector] Unable to inject com/headway/assemblies/seaview/headless/data/KeyMeasureData$JaxbAccessorF_a
java.lang.SecurityException: class "com.headway.assemblies.seaview.headless.data.KeyMeasureData$JaxbAccessorF_a"'s signer information does not match signer information of other classes in the same package
        at java.lang.ClassLoader.checkCerts(ClassLoader.java:891)
        at java.lang.ClassLoader.preDefineClass(ClassLoader.java:661)
        at java.lang.ClassLoader.defineClass(ClassLoader.java:754)
        at java.lang.ClassLoader.defineClass(ClassLoader.java:635)
        at sun.reflect.GeneratedMethodAccessor2.invoke(Unknown Source)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at com.sun.xml.internal.bind.v2.runtime.reflect.opt.Injector.inject(Injector.java:251)
        at com.sun.xml.internal.bind.v2.runtime.reflect.opt.Injector.inject(Injector.java:77)
        at com.sun.xml.internal.bind.v2.runtime.reflect.opt.AccessorInjector.prepare(AccessorInjector.java:72)
        at com.sun.xml.internal.bind.v2.runtime.reflect.opt.OptimizedAccessorFactory.get(OptimizedAccessorFactory.java:164)
        at com.sun.xml.internal.bind.v2.runtime.reflect.Accessor$FieldReflection.optimize(Accessor.java:271)
        at com.sun.xml.internal.bind.v2.runtime.reflect.TransducedAccessor$CompositeTransducedAccessorImpl.<init>(TransducedAccessor.java:220)
        at com.sun.xml.internal.bind.v2.runtime.reflect.TransducedAccessor.get(TransducedAccessor.java:160)
        at com.sun.xml.internal.bind.v2.runtime.property.AttributeProperty.<init>(AttributeProperty.java:76)
        at com.sun.xml.internal.bind.v2.runtime.property.PropertyFactory.create(PropertyFactory.java:93)
        at com.sun.xml.internal.bind.v2.runtime.ClassBeanInfoImpl.<init>(ClassBeanInfoImpl.java:166)
        at com.sun.xml.internal.bind.v2.runtime.JAXBContextImpl.getOrCreate(JAXBContextImpl.java:488)
        at com.sun.xml.internal.bind.v2.runtime.JAXBContextImpl.<init>(JAXBContextImpl.java:305)
        at com.sun.xml.internal.bind.v2.runtime.JAXBContextImpl.<init>(JAXBContextImpl.java:124)
        at com.sun.xml.internal.bind.v2.runtime.JAXBContextImpl$JAXBContextBuilder.build(JAXBContextImpl.java:1123)
        at com.sun.xml.internal.bind.v2.ContextFactory.createContext(ContextFactory.java:147)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at javax.xml.bind.ContextFinder.newInstance(ContextFinder.java:247)
        at javax.xml.bind.ContextFinder.newInstance(ContextFinder.java:234)
        at javax.xml.bind.ContextFinder.find(ContextFinder.java:462)
        at javax.xml.bind.JAXBContext.newInstance(JAXBContext.java:641)
        at javax.xml.bind.JAXBContext.newInstance(JAXBContext.java:584)
        at javax.xml.bind.JAXB$Cache.<init>(JAXB.java:112)
        at javax.xml.bind.JAXB.getContext(JAXB.java:139)
        at javax.xml.bind.JAXB.unmarshal(JAXB.java:153)
        at com.structure101.plugin.sonar.Structure101Sensor.saveV5MeasuresAndIssuesFromSummaryReport(Structure101Sensor.java:106)
        at com.structure101.plugin.sonar.Structure101Sensor.execute(Structure101Sensor.java:93)
        at org.sonar.scanner.sensor.AbstractSensorWrapper.analyse(AbstractSensorWrapper.java:48)
        at org.sonar.scanner.sensor.ModuleSensorsExecutor.execute(ModuleSensorsExecutor.java:85)
        at org.sonar.scanner.sensor.ModuleSensorsExecutor.lambda$execute$1(ModuleSensorsExecutor.java:59)
        at org.sonar.scanner.sensor.ModuleSensorsExecutor.withModuleStrategy(ModuleSensorsExecutor.java:77)
        at org.sonar.scanner.sensor.ModuleSensorsExecutor.execute(ModuleSensorsExecutor.java:59)
        at org.sonar.scanner.scan.ModuleScanContainer.doAfterStart(ModuleScanContainer.java:82)
        at org.sonar.core.platform.ComponentContainer.startComponents(ComponentContainer.java:136)
        at org.sonar.core.platform.ComponentContainer.execute(ComponentContainer.java:122)
        at org.sonar.scanner.scan.ProjectScanContainer.scan(ProjectScanContainer.java:400)
        at org.sonar.scanner.scan.ProjectScanContainer.scanRecursively(ProjectScanContainer.java:395)
        at org.sonar.scanner.scan.ProjectScanContainer.doAfterStart(ProjectScanContainer.java:358)
        at org.sonar.core.platform.ComponentContainer.startComponents(ComponentContainer.java:136)
        ...
```

You can also build the Docker image yourself.
From the root of the project, do:

```bash
docker build -t jzheaux/sonar-and-structure101 src/main/docker/
```

