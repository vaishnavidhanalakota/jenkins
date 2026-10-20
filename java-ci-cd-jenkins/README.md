# Java CI/CD with Jenkins (DevOps Lab)

## Aim
Configure Jenkins to automate checkout, build, test, package, and deployment of a Java Maven application.

## Requirements
- JDK 17 or later
- Git
- Apache Maven
- Jenkins with Pipeline and Git plugins
- Windows Jenkins agent for the supplied Jenkinsfile (`bat` commands)

## Run locally
From this folder in Command Prompt:
```bat
mvn clean test
mvn package
java -cp target\java-ci-cd-1.0.jar com.lab.App
```

Expected output:
`Java application deployed successfully!`

## Configure GitHub
1. Create a GitHub repository named `java-ci-cd`.
2. Replace `YOUR_USERNAME` in the `Jenkinsfile` with your GitHub username.
3. Upload this folder to the repository:
```bat
git init
git add .
git commit -m "Initial Java CI CD project"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/java-ci-cd.git
git push -u origin main
```

## Configure Jenkins
1. Open Jenkins (usually `http://localhost:8080`).
2. Select **New Item**, enter `Java-CI-CD-Pipeline`, choose **Pipeline**, and click **OK**.
3. Under **Pipeline**, select **Pipeline script from SCM**.
4. SCM: **Git**; Repository URL: your GitHub URL; Branch: `*/main`; Script Path: `Jenkinsfile`.
5. Save, then select **Build Now**.
6. Open the build's **Console Output** and check the stages.

## Pipeline stages
- Checkout: fetches source code from GitHub
- Build: compiles source with Maven
- Test: runs JUnit tests and publishes test results
- Package: creates and archives the JAR
- Deploy: copies the JAR into the workspace's `deploy` folder

Note: The Deploy stage is a local lab demonstration, not a remote production deployment. The Jenkinsfile is configured for a Windows agent. For Linux, replace `bat` steps with suitable `sh` commands.

## Automatic triggers
For a basic local lab, enable **Poll SCM** under Build Triggers and use:
`H/5 * * * *`

This checks for changes approximately every five minutes. A GitHub webhook is another option if Jenkins is reachable by GitHub.
