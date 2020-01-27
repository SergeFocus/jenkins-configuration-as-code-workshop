# Exercises

## Task: Use Explicit Version of Jenkins

It is recommended to explicitly use a specific version of Jenkins, even for Jenkins LTS versions. It improves traceability.

Check the version of the Jenkins LTS we are running on the lower left corner of the Jenkins web user interface.

Hints:

```patch
@@ -1,4 +1,4 @@
--- a/0-scratch/jenkins/Dockerfile
+++ b/0-scratch/jenkins/Dockerfile
-FROM jenkins/jenkins:lts
+FROM jenkins/jenkins:2.204.5

 LABEL maintainer="Leonard Sheng Sheng Lee <leonard.sheng.sheng.lee@gmail.com>"

```

- Run `make`. See [Makefile](Makefile) for more information.

- Open [http://localhost:8080](http://localhost:8080) to access Jenkins.
