prerequisites (Before touching Jenkins)

Make sure these are ready:

JDK installed on the Jenkins machine

Maven installed (for Java project)

Git installed

Jenkins is running (with admin access)

A GitHub repository with a Maven Java project

Has a pom.xml

Has some tests (optional but better)

Internet access (so Jenkins can pull dependencies from Maven Central)

2️⃣ Configure Tools in Jenkins (one-time setup)
2.1 Configure JDK

Open Jenkins → Manage Jenkins

Click Tools (or Global Tool Configuration depending on version)

Under JDK:

Click Add JDK

Name: JAVA_HOME

Uncheck Install automatically

Give local JDK path, for example:

Linux: /usr/lib/jvm/java-11-openjdk-amd64

Windows: C:\Program Files\Java\jdk-17

2.2 Configure Maven

Still in Global Tool Configuration

Under Maven:

Click Add Maven

Name: MAVEN_HOME

Option 1: Tick Install automatically → choose version

Option 2: Uncheck, give local Maven path, e.g.:

Linux: /opt/maven

Windows: C:\apache-maven-3.9.0

Click Save.

3️⃣ Prepare GitHub Repository

Your GitHub repo should look like:

my-maven-app/
 ├── src/
 ├── pom.xml
 └── (optional) Jenkinsfile


If you want Jenkins to read the pipeline from GitHub, create a file:

Jenkinsfile (Scripted Pipeline):

node {

    stage('Clone from GitHub') {
        echo "Cloning source code from GitHub..."
        git branch: 'main', url: 'https://github.com/USERNAME/REPO.git'
    }

    stage('Build') {
        echo "Building the project with Maven..."
        // For Linux:
        sh "mvn clean package"
        // For Windows, replace with:
        // bat 'mvn clean package'
    }

    stage('Test') {
        echo "Running unit tests..."
        // For Linux:
        sh "mvn test"
        // For Windows:
        // bat 'mvn test'
    }

    stage('Archive Results') {
        echo "Archiving build artifacts and test reports..."
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        junit 'target/surefire-reports/*.xml'
    }

}


For exam: remember node { ... stage('..'){...} } → Scripted pipeline syntax.

If you don’t want to put Jenkinsfile in GitHub, you can paste this directly in Jenkins later (Step 5).

4️⃣ Create a New Jenkins Pipeline Job

Go to Jenkins Dashboard

Click New Item

Give a name:
maven-github-scripted-pipeline

Select Pipeline

Click OK

You are now in the job configuration page.

5️⃣ Configure Where the Script Comes From

You have two options:

✅ Option A: Pipeline Script from SCM (Recommended)

This assumes Jenkinsfile is in your GitHub repo.

In job config, scroll to Pipeline section

In Definition, select: Pipeline script from SCM

SCM: select Git

Repository URL:
https://github.com/USERNAME/REPO.git

Branch Specifier:
*/main or */master

If the repo is private → add Credentials

Script Path:
Jenkinsfile (default name at root)

Click Save.

✅ Option B: Directly paste Script (No Jenkinsfile in repo)

In job config, under Pipeline

Set Definition: Pipeline script

A big text box appears → paste this Scripted Pipeline:

node {

    stage('Clone from GitHub') {
        echo "Cloning source code from GitHub..."
        git branch: 'main', url: 'https://github.com/USERNAME/REPO.git'
    }

    stage('Build') {
        echo "Building the project with Maven..."
        // Linux:
        sh "mvn clean package"
        // Windows alternative:
        // bat 'mvn clean package'
    }

    stage('Test') {
        echo "Running unit tests..."
        // Linux:
        sh "mvn test"
        // Windows:
        // bat 'mvn test'
    }

    stage('Archive Results') {
        echo "Archiving build artifacts and test reports..."
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        junit 'target/surefire-reports/*.xml'
    }

}


Click Save.

6️⃣ Run the Pipeline

Go to the job page

Click Build Now

Jenkins will:

Allocate a node (agent)

Run the node { ... } block

Execute each stage {} in order

You can see progress:

Left side → Build History → click latest build (e.g. #1)

Click Console Output

You will see logs like:

"Cloning repository"

"Downloading from central"

"Building jar"

"Running tests"

"Archiving artifacts"