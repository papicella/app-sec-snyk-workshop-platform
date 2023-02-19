# Snyk Application Security Hands-On Workshop

The following workshop is designed to show how Snyk integrates into SCM systems like GitHub and performs various application security scans and what fix/remediation advice is given to secure you applications during the SDLC. 

This covers four of the Snyk Products as listed below:

* Snyk Open Source
* Snyk Code
* Snyk Container
* Snyk IaC

## Prerequisites

* public GitHub account - http://github.com
* git CLI - https://git-scm.com/downloads
* snyk CLI - https://support.snyk.io/hc/en-us/articles/360003812538-Install-the-Snyk-CLI
* Registered account on Snyk App - http://app.snyk.io
* Maven installed - https://maven.apache.org/download.cgi
* install snyk-to-html tool - https://docs.snyk.io/products/snyk-code/cli-for-snyk-code/displaying-the-cli-results-in-an-html-format-using-the-snyk-to-html-feature/installing-the-snyk-to-html-tool

## What we will do in this hands-on workshop?

In this workshop we will use the Snyk Platform to monitor and perform application security scans across various different artifacts in the repository. This workshop will focus on Snyk Open Source, Snyk Code, Snyk Container and Snyk IaC capability.

* [Step 1 - Fork our sample repo into your own GitHub account](#step-1---fork-our-sample-repo-into-your-own-github-account)
* [Step 2 - Configure GitHub Integration](#step-2---configure-github-integration)
* [Step 3 - Analyze Snyk Open Source Scan Results](#step-3---analyze-snyk-open-source-scan-results)
* [Step 4 - Analyze Snyk Code Scan Results](#step-4---analyze-snyk-code-scan-results) 
* [Step 5 - Fix a Vulnerability Using Snyk's Pull Request feature](#step-5---fix-a-vulnerability-using-snyks-pull-request-feature)
* [Step 6 - Perform Snyk Test Using Snyk Open Source](#step-6---perform-snyk-test-using-snyk-open-source)
* [Step 7 - Perform a Snyk Test Using Snyk Code](#step-7---perform-a-snyk-test-using-snyk-code)
* [Step 8 - Using Snyk VS Code IDE Plugin](#step-8---using-snyk-vs-code-ide-plugin)
* Step 9 - Analyze Snyk IaC Scan Results
* Step 10 - Perform Snyk Test Using Snyk IaC
* Step 11 - Analyze Dockerfile Scan Results
* Step 12 - Analyze a Container using Snyk Container Registry Scan

# Workshop Steps

_Note: It is assumed your using a mac for these steps, but it should also work on Windows or linux with some modifications to the scripts potentially_

## Step 1 - Fork our sample repo into your own GitHub account

Navigate to the following GitHub repo - https://github.com/papicella/snyk-boot-web

* Click on the "**Fork**" button
* Ensure you are forking this repo to your public GitHub account
* Click done

![alt tag](https://i.ibb.co/JdvF8pP/app-sec-snyk-workshop-1.png)

## Step 2 - Configure GitHub Integration

_NOTE: You may have already setup GitHub integration in that case go ahead and skip this step_

* Login to http://app.snyk.io Sign up if you haven't already.
* Navigating to Integrations -> Source Control -> GitHub
* Fill in your Account Credentials to Connect your GitHub Account.

![alt tag](https://i.ibb.co/0qmpjYT/platform-workshop-2.png)

Now that Snyk is connected to your GitHub Account, import the Repo into Snyk as a Project.

* Navigate to Projects menu option
* Click "**Add Project**" then select "**GitHub**"
* Click on the Repo you forked.

![alt tag](https://i.ibb.co/q9Rsxsh/snyk-starter-open-source-3.png)

![alt tag](https://i.ibb.co/f9JsRQX/app-sec-snyk-workshop-2.png)

_Note: The import can take up to one minute so you can view the import log while it's running_

![alt tag](https://i.ibb.co/0JK5jWD/platform-workshop-1.png)

* Finally, ensure you have enabled Snyk Code under the Settings menu option as shown below, before moving onto the next step

![alt tag](https://i.ibb.co/Nn540GL/platform-workshop-3.png)

The scan should not take longer then a few minutes once complete more onto the next step below

## Step 3 - Analyze Snyk Open Source Scan Results

Now we have imported our **snyk-boot-web** repo into Snyk let's take a look at the scan results for our maven manifest pom.xml file where our open source dependencies are declared.

* Click on the pom.xml as shown below

![alt tag](https://i.ibb.co/wM1Bnm3/platform-workshop-4.png)

Let's have a look at the vulnerabilities.

For each Vulnerability, Snyk displays the following ordered by our [Proprietary Priority Score](https://docs.snyk.io/features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score) :
1. The module that introduced it and, in the case of transitive dependencies, its direct dependency,
2. Details on the path and proposed Remediation, as well as the specific vulnerable functions
3. Overview
4. Exploit maturity
5. Links to CWE, CVE and CVSS Score
6. A link to a Snyk Learn module on how to fix these type of vulnerabilities if available
7. The ability to ignore issues you wish to remove from the list
8. Plus more ...

![alt tag](https://i.ibb.co/Y030hc4/app-sec-snyk-workshop-7.png)

## Step 4 - Analyze Snyk Code Scan Results

* Now let's return to the projects view page
* Click on "**Code Analysis**" to view our SAST scan results as shown below

![alt tag](https://i.ibb.co/Fw6LR5q/platform-workshop-5.png)

For each Vulnerability, Snyk displays the following:

1. Each Vulnerability grouped by severity
2. Each Vulnerability links to the CWE category code
3. Each Vulnerability shows the CWE category name
4. Displays the line of code where the security issue exists
5. Description for the issue and the code file name it exists in
6. A link to a Snyk Learn module on how to fix these type of vulnerabilities if available
7. The ability to ignore issues you wish to remove from the list

![alt tag](https://i.ibb.co/xCjvm7g/app-sec-snyk-workshop-9.png)

There is only a single SQL Injection vulnerability in our code for this repo. * Click on the "**Full Details**" button to reveal full details as shown below.

![alt tag](https://i.ibb.co/FVxJ48Z/app-sec-snyk-workshop-10.png)

All Snyk products provide a developer-friendly experience, so Snyk Code helps developers to quickly understand the problem, learn the background, and how to approach it. Snyk Code helps you understand the dangerous code flow step-by-step. For every issue, Code also provides a link to the lines in the relevant files, to view more details on the problem like the CWE, and how to approach it.

* Click on "**Fix Analysis**" to see how you can fix the issue based on other open source projects. On this page you get not just source code example fixes but also the following detailed information.

1. Details
2. Types Of Attacks and/or Best practices for prevention
3. Affected Environments if applicable

![alt tag](https://i.ibb.co/1KSFGyL/app-sec-snyk-workshop-11.png)

## Step 5 - Fix a Vulnerability Using Snyk's Pull Request feature

When using our Source Code Management integration such as our GitHub integration, and if a fix is available, Snyk can automatically upgrade the vulnerable dependency to a non-vulnerable version through a Pull Request.

* Let's return to the project view page
* Once again click on "**pom.xml**" to reveal it's vulnerabilities page, so we can fix one of our issues
* In the search bar type in "**log4j**"
* Click on "**Fix this vulnerability**" for "**log4j**" issue as shown below

![alt tag](https://i.ibb.co/rwzGZgS/app-sec-snyk-workshop-12.png)

* On the next screen, you'll be able to confirm the issue to fix with this PR. Click "**Open a Fix PR**" at the bottom of the page

![alt tag](https://i.ibb.co/2kKqwwz/app-sec-snyk-workshop-13.png)

* Once it's ready, you'll be taken to the PR in GitHub, where you can review the changes in the file diff view:

![alt tag](https://i.ibb.co/q1MxC1S/app-sec-snyk-workshop-14.png)

![alt tag](https://i.ibb.co/0KpzJRN/app-sec-snyk-workshop-16.png)

* We see that PR checks completed successfully, ensuring us we didn't introduce a breaking change

![alt tag](https://i.ibb.co/z4v4KDx/app-sec-snyk-workshop-15.png)

* Optionally now, go ahead and merge the PR!
* Back in Snyk we can appreciate that our "**pom.xml**" file has 1 less Critical Severity Vulnerability if you did fix it

## Step 6 - Perform Snyk Test Using Snyk Open Source

In addition to the Snyk App UI we also have the snyk CLI a build-time tool to find & fix known vulnerabilities in open-source dependencies. The CLI is what is used in DevOps pipelines to introduce Application Security Scans as part of that workflow to push applications into production.

Install the relevant package manager before you use the Snyk CLI tool. In this case you will need maven installed to perform these steps

```bash
$ mvn --version
Apache Maven 3.8.4 (9b656c72d54e5bacbed989b64718c159fe39b537)
Maven home: /opt/homebrew/Cellar/maven/3.8.4/libexec
Java version: 11.0.13, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk-11.0.13.jdk/Contents/Home
Default locale: en_AU, platform encoding: UTF-8
OS name: "mac os x", version: "11.3", arch: "x86_64", family: "mac"
```

* Before we get started please make sure you have setup the Snyk CLI. There are various install options as per the links below. Using the prebuilt binaries means you don't have to install NPM to install the Snyk CLI.

1. Install Page - https://support.snyk.io/hc/en-us/articles/360003812538-Install-the-Snyk-CLI
1. Prebuilt Binaries - https://github.com/snyk/snyk/releases

_Note: Make sure you have the following version installed or later_

```bash
$ snyk --version
1.1105.0
```

* Authorize the snyk CLI with your account as follows

```bash
$ snyk auth

Now redirecting you to our auth page, go ahead and log in,
and once the auth is complete, return to this prompt and you'll
be ready to start using snyk.

If you can't wait use this url:
https://app.snyk.io/login?token=....


Your account has been authenticated. Snyk is now ready to be used.
```

_Note: If you are having trouble authenticating via a browser with the Snyk App you can setup authentication using the API token as shown below
[Authenticate using your API token](https://docs.snyk.io/snyk-cli/authenticate-the-cli-with-your-account)_

* Clone your forked repository as shown below. You would use your own GitHub repo here instead of the one shown below

```bash
$ git clone https://github.com/papicella/snyk-boot-web
Cloning into 'snyk-boot-web'...
remote: Enumerating objects: 145, done.
remote: Counting objects: 100% (145/145), done.
remote: Compressing objects: 100% (103/103), done.
remote: Total 145 (delta 60), reused 91 (delta 22), pack-reused 0
Receiving objects: 100% (145/145), 74.51 KiB | 2.76 MiB/s, done.
Resolving deltas: 100% (60/60), done.
```

* Change to the "**snyk-boot-web**" directory

```bash
$ cd snyk-boot-web
```

* To have better control over your tests, you can pass the severity-threshold flag to the snyk test command with one of the supported options (low|medium|high|critical). With this flag, only vulnerabilities of provided level or higher will be reported. Let's set that to "**critical**" and run a test as shown below.

```bash
$ snyk test --severity-threshold=high

Testing /Users/pasapicella/snyk/SE/workshops/NEW-WORKSHOPS/snyk-boot-web...

Tested 40 dependencies for known issues, found 11 issues, 11 vulnerable paths.

Issues to fix by upgrading:

  Upgrade com.h2database:h2@1.4.200 to com.h2database:h2@2.1.210 to fix
  ✗ Remote Code Execution (RCE) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-2331071] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
  ✗ XML External Entity (XXE) Injection [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-1769238] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
  ✗ Remote Code Execution (RCE) [Critical Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-2348247] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200

  Upgrade org.apache.logging.log4j:log4j-core@2.15.0 to org.apache.logging.log4j:log4j-core@2.17.0 to fix
  ✗ Denial of Service (DoS) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2321524] in org.apache.logging.log4j:log4j-core@2.15.0
    introduced by org.apache.logging.log4j:log4j-core@2.15.0
  ✗ Remote Code Execution (RCE) [Critical Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2320014] in org.apache.logging.log4j:log4j-core@2.15.0
    introduced by org.apache.logging.log4j:log4j-core@2.15.0

  Upgrade org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE to org.springframework.boot:spring-boot-starter-web@2.5.12 to fix
  ✗ Denial of Service (DoS) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMFASTERXMLJACKSONCORE-2421244] in com.fasterxml.jackson.core:jackson-databind@2.11.4
    introduced by org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter-json@2.3.10.RELEASE > com.fasterxml.jackson.core:jackson-databind@2.11.4
  ✗ Privilege Escalation [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHETOMCATEMBED-2414084] in org.apache.tomcat.embed:tomcat-embed-core@9.0.45
    introduced by org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter-tomcat@2.3.10.RELEASE > org.apache.tomcat.embed:tomcat-embed-core@9.0.45
  ✗ Improper Input Validation [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGGLASSFISH-1297098] in org.glassfish:jakarta.el@3.0.3
    introduced by org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter-tomcat@2.3.10.RELEASE > org.glassfish:jakarta.el@3.0.3
  ✗ Remote Code Execution [Critical Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGSPRINGFRAMEWORK-2436751] in org.springframework:spring-beans@5.2.14.RELEASE
    introduced by org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE > org.springframework:spring-web@5.2.14.RELEASE > org.springframework:spring-beans@5.2.14.RELEASE


Issues with no direct upgrade or patch:
  ✗ Remote Code Execution (RCE) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-COMH2DATABASE-31685] in com.h2database:h2@1.4.200
    introduced by com.h2database:h2@1.4.200
  No upgrade or patch available
  ✗ Denial of Service (DoS) [High Severity][https://security.snyk.io/vuln/SNYK-JAVA-ORGYAML-2806360] in org.yaml:snakeyaml@1.26
    introduced by org.springframework.boot:spring-boot-starter-web@2.3.10.RELEASE > org.springframework.boot:spring-boot-starter@2.3.10.RELEASE > org.yaml:snakeyaml@1.26
  This issue was fixed in versions: 1.31


Organization:      pas.apicella-41p
Package manager:   maven
Target file:       pom.xml
Project name:      com.example:snyk-boot-web
Open source:       no
Project path:      /Users/pasapicella/snyk/SE/workshops/NEW-WORKSHOPS/snyk-boot-web
Licenses:          enabled
```

* We can instruct the Snyk App to actually monitor our "**pom.xml**" in the Snyk App UI as shown below, so run "**snyk monitor**" to achieve that. Your Org name can be retrieved using the settings page on your Org in Snyk App.

_Note: You may not need to set the parameter **--org** if you only have the one org in your account._ 

```bash
$ snyk monitor --org=workshops-admin-org

Monitoring /Users/pasapicella/snyk/SE/workshops/NEW-WORKSHOPS/snyk-boot-web (com.example:snyk-boot-web)...

Explore this snapshot at https://app.snyk.io/org/workshops-admin-org/project/c6fa0f1e-acf7-4e89-9957-ef8f227c6e09/history/79490f97-c20f-4931-b7ac-a60db1a9c847

Notifications about newly disclosed issues related to these dependencies will be emailed to you.
```

* Returning to the Snyk App UI will show our CLI "**snyk monitor**" result but this time we didn't use the GitHub integration instead the scan type is given as a CLI scan as we performed this from the CLI itself

![alt tag](https://i.ibb.co/5MSRxhQ/platform-workshop-6.png)

* Finally, lets run a scan and output the results to HTML. You must have installed the [snyk-to-html](https://docs.snyk.io/products/snyk-code/cli-for-snyk-code/displaying-the-cli-results-in-an-html-format-using-the-snyk-to-html-feature/installing-the-snyk-to-html-tool) add on for this to work

```bash
$ snyk test --json | snyk-to-html -o results.html
Vulnerability snapshot saved at results.html
$ open -a "Google Chrome" results.html
```

![alt tag](https://i.ibb.co/LdyK6Zs/app-sec-snyk-workshop-17.png)

## Step 7 - Perform a Snyk Test Using Snyk Code

* To perform a Snyk Code test using the SNYK CLI we simply run "**snyk code test**" from the same directory we are in based on the last step which is the root folder of our cloned repo

```bash
$ snyk code test

Testing /Users/pasapicella/snyk/SE/workshops/NEW-WORKSHOPS/snyk-boot-web ...

 ✗ [High] SQL Injection
   Path: src/main/java/com/example/snykbootweb/jdbc/CustomerRest.java, line 29
   Info: Unsanitized input from the request URL flows into query, where it is used in an SQL query. This may result in an SQL Injection vulnerability.


✔ Test completed

Organization:      pas.apicella-41p
Test type:         Static code analysis
Project path:      /Users/pasapicella/snyk/SE/workshops/NEW-WORKSHOPS/snyk-boot-web

Summary:

  1 Code issues found
  1 [High]
```

* Finally, lets run a snyk code scan and output the results to HTML

```bash
$ snyk code test --json | snyk-to-html -o results.html
Vulnerability snapshot saved at results.html
$ open -a "Google Chrome" results.html
```

![alt tag](https://i.ibb.co/YdB7tPX/app-sec-snyk-workshop-18.png)

## Step 8 - Using Snyk VS Code IDE Plugin

Optionally if you have time, and you have VS Code installed you can install a plugin to allow you to scan your "**snyk-boot-web**" code within VS code while in an IDE. Of course if you prefer to use IntelliJ IDEA then feel free to use that. 

* Install it using the following link - [Install VS Code Snyk Plugin](https://marketplace.visualstudio.com/items?itemName=snyk-security.vscode-vuln-cost)
* If using IntelliJ IDEA - [Install JetBrains Snyk Plugin](https://plugins.jetbrains.com/plugin/10972-snyk-security--code-open-source-container-iac-configurations)

* _Note: Once installed ensure you authenticate with Snyk App prior to running your first IDE scan_

Here are some links showing you how to do this

1. IntelliJ IDEA - https://docs.snyk.io/ide-tools/jetbrains-plugins/authentication-for-the-jetbrains-plugins
2. VS Code - https://docs.snyk.io/ide-tools/visual-studio-code-extension/visual-studio-code-extension-authentication

_VS Code_

![alt tag](https://i.ibb.co/zmFGMMg/app-sec-snyk-workshop-5.png)

_IntelliJ IDEA_

![alt tag](https://i.ibb.co/ZY3Fr89/app-sec-snyk-workshop-20.png)

## Step 9 - Analyze Snyk IaC Scan Results

Snyk Infrastructure as Code allows you to find and fix vulnerabilities in your Kubernetes, Helm, Terraform, CloudFormation and Arm Templates configuration files

* Return to the projects page and you will see various type of IaC scans from our already imported repo "**snyk-boot-web**". Go ahead and click on the terraform file as shown below to view it's scan results.

![alt tag](https://i.ibb.co/Pg37Yz1/platform-workshop-7.png)

For each Vulnerability, Snyk displays the following ordered by Highest Severity:

1. Each Vulnerability grouped by line no and severity
2. Each Vulnerability links to the Snyk policy it was defined against including the path to the issue, what the issue is, the impact and how to resolve it
3. The ability to ignore issues you wish to remove from the list

![alt tag](https://i.ibb.co/Z88GTDH/platform-workshop-8.png)

![alt tag](https://i.ibb.co/rxtNMjR/platform-workshop-9.png)

Note: We will resolve some of these issues shortly for now just browse through some of them to get familiar with what was raised and why including clicking on the Snyk Policy links

## Step 10 - Perform Snyk Test Using Snyk IaC

* At this point let's go ahead and test "**main.tf**" to do that issue a command as shown below. In this example we are testing that file itself by specifically referring to it in the command.

```bash
$ snyk iac test ./terraform/main.tf

Snyk Infrastructure as Code

Using custom rules to generate misconfigurations.

✔ Test completed.

Issues

Low Severity Issues: 3

  [Low] S3 bucket versioning disabled
  Info:    S3 bucket versioning is disabled. Changes or deletion of objects will
           not be reversible
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-124
  Path:    resource > aws_s3_bucket[s3_bucket_myapp] > versioning > enabled
  File:    ./terraform/main.tf
  Resolve: For AWS provider < v4.0.0, set `versioning.enabled` attribute to
           `true`. For AWS provider >= v4.0.0, add aws_s3_bucket_versioning
           resource.

  [Low] S3 bucket MFA delete control disabled
  Info:    S3 bucket will not enforce MFA login on delete requests. Object could
           be deleted without stronger MFA authorization
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-127
  Path:    resource > aws_s3_bucket[s3_bucket_myapp] > versioning > mfa_delete
  File:    ./terraform/main.tf
  Resolve: Follow instructions in `https://docs.aws.amazon.com/AmazonS3/latest/u
           serguide/MultiFactorAuthenticationDelete.html` to manually configure
           the MFA setting. For AWS provider < v4.0.0 set
           `versioning.mfa_delete` attribute to `true` in aws_s3_bucket
           resource. For AWS provider >= v4.0.0 set
           'versioning_configuration.mfa_delete` attribute to `Enabled`. The
           terraform change is required to reflect the setting in the state file

  [Low] S3 server access logging is disabled
  Info:    The s3 access logs will not be collected. There will be no audit
           trail of access to s3 objects
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-45
  Path:    input > resource > aws_s3_bucket[s3_bucket_myapp] > logging
  File:    ./terraform/main.tf
  Resolve: For AWS provider < v4.0.0, add `logging` block attribute. For AWS
           provider >= v4.0.0, add aws_s3_bucket_logging resource.

Medium Severity Issues: 2

  [Medium] Missing an owner from tag
  Rule:    custom rule MY_RULE_1
  Path:    input > resource > aws_s3_bucket[s3_bucket_myapp] > tags
  File:    ./terraform/main.tf

  [Medium] Non-encrypted S3 Bucket
  Info:    Non-encrypted S3 Bucket. A non-encrypted S3 bucket increases the
           likelihood of unintentional data exposure
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-4
  Path:    input > resource > aws_s3_bucket[s3_bucket_myapp]
  File:    ./terraform/main.tf
  Resolve: For AWS provider < v4.0.0, set `server_side_encryption_configuration`
           block attribute. For AWS provider >= v4.0.0 add
           aws_s3_bucket_server_side_encryption_configuration resource.

High Severity Issues: 1

  [High] S3 block public ACLs control is disabled
  Info:    Bucket does not prevent creation of public ACLs. Anyone who can
           manage bucket's ACLs will be able to grant public access to the
           bucket
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-95
  Path:    resource > aws_s3_bucket[s3_bucket_myapp]
  File:    ./terraform/main.tf
  Resolve: Set the `aws_s3_bucket_public_access_block` `block_public_acls` field
           to true.

-------------------------------------------------------

Test Summary

  Organization: pas.apicella-41p
  Project name: papicella/snyk-boot-web

✔ Files without issues: 0
✗ Files with issues: 1
  Ignored issues: 0
  Total issues: 6 [ 0 critical, 1 high, 2 medium, 3 low ]

-------------------------------------------------------

Tip

  New: Share your test results in the Snyk Web UI with the option --report
```

* Go ahead and fix any of these issues using the provided remediation, you acn go back to Snyk App UI should you find the remediation advice on the UI easier to read
* Finally like all Snyk CLI scans you can set a severity threshold to indicate when we would like to break a build within a CI/CD pipeline as shown below

```bash
$ snyk iac test ./terraform/main.tf --severity-threshold=high

Snyk Infrastructure as Code

Using custom rules to generate misconfigurations.

✔ Test completed.

Issues

High Severity Issues: 1

  [High] S3 block public ACLs control is disabled
  Info:    Bucket does not prevent creation of public ACLs. Anyone who can
           manage bucket's ACLs will be able to grant public access to the
           bucket
  Rule:    https://snyk.io/security-rules/SNYK-CC-TF-95
  Path:    resource > aws_s3_bucket[s3_bucket_myapp]
  File:    ./terraform/main.tf
  Resolve: Set the `aws_s3_bucket_public_access_block` `block_public_acls` field
           to true.

-------------------------------------------------------

Test Summary

  Organization: pas.apicella-41p
  Project name: papicella/snyk-boot-web

✔ Files without issues: 0
✗ Files with issues: 1
  Ignored issues: 0
  Total issues: 1 [ 0 critical, 1 high, 0 medium, 0 low ]

-------------------------------------------------------

Tip

  New: Share your test results in the Snyk Web UI with the option --report
```

## Step 11 - Analyze Dockerfile Scan Results

Snyk detects vulnerable base images by scanning your Dockerfile when importing a Git repository. This allows you to examine security issues before building the image, so helps solve potential problems before they land in your registry or in production.

* Go ahead and return to the Projects page and this time click on the Dockerfile scan result as shown below

![alt tag](https://i.ibb.co/BfwRHJ3/platform-workshop-10.png)

* Here we will go ahead and fix our Dockerfile using the "Open a Fix PR" button as follows

![alt tag](https://i.ibb.co/n0LhyFn/platform-workshop-11.png)

* Click on "Open a Fix PR" on the resulting page as shown below

![alt tag](https://i.ibb.co/bQLz6nq/platform-workshop-12.png)

* A PR is then created as show below. "**Files Changed**" will show you what it's updating in the Dockerfile itself

![alt tag](https://i.ibb.co/4sDBzyV/platform-workshop-13.png)

* Return to the projects dashboard, and you will see a new scan has occurred automatically and now our Dockerfile shows much less issues than previously. Of course until we build a new container and add it to the registry the container itself will still have the old base image in place within the Container registry itself.

![alt tag](https://i.ibb.co/HzNSSbF/platform-workshop-14.png)

Snyk Container allows you to scan a Dockerfile as shown above as well as directly into a Container registry or through Snyk's Kubernetes Integration as well as using the Snyk CLI which is described here.

[Snyk Container Integrations](https://docs.snyk.io/scan-containers/snyk-container-integrations)

## Step 12 - Analyze a Container using Snyk Container Registry Scan

Thanks for attending and completing this workshop

![alt tag](https://i.ibb.co/qJFDfWP/snyk-thumb.jpg)

<hr />
Pas Apicella [pas at snyk.io] is a Principal Solution Engineer APJ at Snyk
