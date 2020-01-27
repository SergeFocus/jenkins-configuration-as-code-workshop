# Exercises

## Task: Review Administrative Monitors (See Upper Right Square Numeric Red Box)

We notice that there are few active administrative monitors, shown when we click on the red box. How could we fix some of them by Jenkins Configuration as Code (JCasC)?

### Task: Fix Jenkins Root URL

```text
Jenkins root URL is empty but is required for the proper operation of many Jenkins features like email notifications, PR status update, and environment variables such as BUILD_URL.

Please provide an accurate value in Jenkins configuration.
```

Hints:

You can configure system manually first to explore how the configuration is being used.

Go to `Jenkins` > `Manage Jenkins` > [Configure System](http://localhost:8080/configure).

Enter `http://localhost:8080` for `Jenkins URL` input field under `Jenkins Location`.

Enter your email for `System Admin e-mail address` input field under `Jenkins Location`.

Go to `Jenkins` > `Manage Jenkins` > [Configuration as Code](http://localhost:8080/configuration-as-code/).

Click `View Configuration` to verify the applied configuration.

```patch
--- a/0-scratch/jenkins/jenkins.yaml
+++ b/0-scratch/jenkins/jenkins.yaml
@@ -8,3 +8,8 @@ jenkins:
     Welcome to Jenkins!    ٩(◕‿◕)۶
     This Jenkins was configured with Jenkins Configuration as Code plugin.
     You can freely modify its configuration without repercussion.
+
+unclassified:
+  location:
+    adminAddress: "Leonard Sheng Sheng Lee <leonard.sheng.sheng.lee@gmail.com>"
+    url: "http://localhost:8080"
```

### Task: Set Up Security

- Create a `secrets.env` file inside `jenkins` directory with below content. Ignore the empty values at this stage.

```text
JENKINS_SSH_PRIVATE_KEY_PASSWORD=
JENKINS_ADMINISTRATOR_USERNAME=
JENKINS_ADMINISTRATOR_PASSWORD=
LDAP_SERVICE_USERNAME=
LDAP_SERVICE_PASSWORD=
NEXUS_USERNAME=
NEXUS_USERPASSWORD=
```

```text
Jenkins is currently unsecured and allows anyone on the network to launch processes on your behalf. It is recommended to set up security and to limit anonymous access even on private networks.
```

You can set up security manually first to explore how the configuration is being used.

Go to `Jenkins` > `Manage Jenkins` > [Configure Global Security](http://localhost:8080/configureSecurity/).

Enable `Logged-in users can do anything` and `Allow anonymous read access` under `Authorization`.

Go to `Jenkins` > `Manage Jenkins` > [Configuration as Code](http://localhost:8080/configuration-as-code/).

Click `View Configuration` to verify the applied configuration.

```patch
--- a/0-scratch/jenkins/jenkins.yaml
+++ b/0-scratch/jenkins/jenkins.yaml
@@ -8,3 +8,11 @@ jenkins:
     Welcome to Jenkins!    ٩(◕‿◕)۶
     This Jenkins was configured with Jenkins Configuration as Code plugin.
     You can freely modify its configuration without repercussion.
+  authorizationStrategy: "loggedInUsersCanDoAnything"
+  securityRealm:
+    local:
+      allowsSignup: false
+      enableCaptcha: false
+      users:
+        - id: ${JENKINS_ADMINISTRATOR_USERNAME:-administrator}
+          password: ${JENKINS_ADMINISTRATOR_PASSWORD:-changeit}
```

- Run `make`. See [Makefile](Makefile) for more information.

- Open [http://localhost:8080](http://localhost:8080) to access Jenkins.

### Task: Resolve CSRF Issuer

```text
You have not configured the CSRF issuer. This could be a security issue. For more information, please refer to this page.
You can change the current configuration using the Security section CSRF Protection.
```

Hints:

You can enable CSRF Protection manually first to explore how the configuration is being used.

Go to `Jenkins` > `Manage Jenkins` > [Configure Global Security](http://localhost:8080/configureSecurity/).

Enable `Prevent Cross Site Request Forgery exploits` under `CSRF Protection`.

Go to `Jenkins` > `Manage Jenkins` > [Configuration as Code](http://localhost:8080/configuration-as-code/).

Click `View Configuration` to verify the applied configuration.

```patch
--- a/0-scratch/jenkins/jenkins.yaml
+++ b/0-scratch/jenkins/jenkins.yaml
@@ -8,3 +8,4 @@ jenkins:
     Welcome to Jenkins!    ٩(◕‿◕)۶
     This Jenkins was configured with Jenkins Configuration as Code plugin.
     You can freely modify its configuration without repercussion.
+  crumbIssuer: "standard"
```

- Run `make`. See [Makefile](Makefile) for more information.

- Open [http://localhost:8080](http://localhost:8080) to access Jenkins.
