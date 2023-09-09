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

---

```bash
➤ mvn quarkus:add-extension -Dextensions="io.quarkus:quarkus-kubernetes"                                                                                                                                                                           02:12:22
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< io.weli:play-quarkus-k8s >----------------------
[INFO] Building play-quarkus-k8s 0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- quarkus-maven-plugin:1.0.0.Final:add-extension (default-cli) @ play-quarkus-k8s ---
✅ Adding dependency io.quarkus:quarkus-kubernetes:jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.977 s
[INFO] Finished at: 2023-09-10T02:12:26+08:00
[INFO] ------------------------------------------------------------------------
weli@192:~/w/play-quarkus-k8s|main⚡*?
➤ git diff                                                                                                                                                                                                                                         02:12:26
diff --git a/pom.xml b/pom.xml
index a4d63ca..918390f 100644
--- a/pom.xml
+++ b/pom.xml
@@ -44,6 +44,10 @@
       <artifactId>rest-assured</artifactId>
       <scope>test</scope>
     </dependency>
+    <dependency>
+      <groupId>io.quarkus</groupId>
+      <artifactId>quarkus-kubernetes</artifactId>
+    </dependency>
   </dependencies>
   <build>
     <plugins>
```

---

```bash
➤ mvn package -DskipTests
...
[INFO] [org.jboss.threads] JBoss Threads version 3.0.0.Final
[INFO] Initializing dekorate session.
[INFO] Default s2i build generator....
[INFO] Registering s2i handler!
[INFO] Generating manifests.
[INFO] Processing kubernetes configuration.
[INFO] Processing openshift configuration.
[INFO] Processing s2i configuration.
[INFO] Closing dekorate session.
[INFO] [io.quarkus.deployment.pkg.steps.JarResultBuildStep] Building thin jar: /Users/weli/works/play-quarkus-k8s/target/play-quarkus-k8s-0.1-SNAPSHOT-runner.jar
[INFO] [io.quarkus.deployment.QuarkusAugmentor] Quarkus augmentation completed in 1434ms
```

---

```bash
➤ ls target/kubernetes/
kubernetes.json
kubernetes.yml
```

---

```yaml
➤ cat target/kubernetes/kubernetes.yml
apiVersion: "v1"
kind: "List"
items:
- apiVersion: "v1"
  kind: "Service"
  metadata:
    labels:
      app: "play-quarkus-k8s"
      version: "0.1-SNAPSHOT"
      group: "weli"
    name: "play-quarkus-k8s"
  spec:
    ports:
    - name: "http"
      port: 8080
      targetPort: 8080
    selector:
      app: "play-quarkus-k8s"
      version: "0.1-SNAPSHOT"
      group: "weli"
    type: "ClusterIP"
- apiVersion: "apps/v1"
  kind: "Deployment"
  metadata:
    labels:
      app: "play-quarkus-k8s"
      version: "0.1-SNAPSHOT"
      group: "weli"
    name: "play-quarkus-k8s"
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: "play-quarkus-k8s"
        version: "0.1-SNAPSHOT"
        group: "weli"
    template:
      metadata:
        labels:
          app: "play-quarkus-k8s"
          version: "0.1-SNAPSHOT"
          group: "weli"
      spec:
        containers:
        - env:
          - name: "KUBERNETES_NAMESPACE"
            valueFrom:
              fieldRef:
                fieldPath: "metadata.namespace"
          image: "weli/play-quarkus-k8s:0.1-SNAPSHOT"
          imagePullPolicy: "IfNotPresent"
          name: "play-quarkus-k8s"
          ports:
          - containerPort: 8080
            name: "http"
            protocol: "TCP"
```

