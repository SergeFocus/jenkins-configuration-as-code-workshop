# Exercises

## Task: Use Jenkins Configuration as Code (JCasC) Plugin

It is important that we have included `configuration-as-code:1.35` in the configuration. Otherwise, Jenkins cannot process our Jenkins Configuration as Code's [jenkins/jenkins.yaml](jenkins/jenkins.yaml) file. Note that we have a predefined system message in [jenkins/jenkins.yaml](jenkins/jenkins.yaml) file.

### Task: Include Jenkins Configuration as Code (JCasC) Plugin

- Verify that `configuration-as-code:1.36` line is included into [jenkins/plugins.txt](jenkins/plugins.txt).

- Run `make`. See [Makefile](Makefile) for more information.

- Open [http://localhost:8080](http://localhost:8080) to access Jenkins.

Was the configured system message shown?

### Task: Exclude Jenkins Configuration as Code (JCasC) Plugin

Try running `make` again __withoout__ `configuration-as-code:1.36` being included.

```patch
--- a/exercise-a_foundation/jenkins/plugins.txt
+++ b/exercise-a_foundation/jenkins/plugins.txt
@@ -4,7 +4,6 @@ bouncycastle-api:2.18
 build-timeout:1.19
 cloudbees-folder:6.11
 command-launcher:1.4
-configuration-as-code:1.36
 credentials-binding:1.20
 email-ext:2.68
 git:4.1.1
```

- Run `make`. See [Makefile](Makefile) for more information.

- Open [http://localhost:8080](http://localhost:8080) to access Jenkins.

Was the earlier configured system message shown now?
