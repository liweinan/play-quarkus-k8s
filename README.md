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

