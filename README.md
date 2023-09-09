# play-quarkus-k8s

```bash
$ mvn io.quarkus:quarkus-maven-plugin:1.0.0.Final:create \
-DprojectGroupId=io.weli \
-DprojectArtifactId=play-quarkus-k8s \
-DprojectVersion=0.1-SNAPSHOT \
-Dendpoint=/hello \
-DclassName=io.weli.Hello
```

---

```bash
$ mvn quarkus:add-extension -Dextensions="io.quarkus:quarkus-kubernetes"
```