1. Create Maven Java Project in Eclipse
Step 1: Create a Maven Project
File → New → Maven Project


✔ Select Create a simple project
✔ Click Next

Fill details:

Field	Value
Group Id	com.example
Artifact Id	MavenJavaProject
Packaging	jar

Click Finish.

Step 2: Create Package and Class

Right-click:

src/main/java → New → Package


Package name:

com.example.app


Now create class:

com.example.app → New → Class


Name: MainApp

Tick ✔ public static void main(String[] args)

Step 3: Add Java Code
package com.example.app;

public class MainApp {
    public static void main(String[] args) {
        System.out.println("Hello from Maven Java Project!");
    }
}

Step 4: Run the Application

Right-click MainApp.java →

Run As → Java Application


Expected Output:

Hello from Maven Java Project!

 2. Push Maven Project to GitHub
Step 1: Locate Project Folder

Right-click project → Properties → Resource

Copy path, for example:

C:\Users\YourName\eclipse-workspace\MavenJavaProject

Step 2: Initialize Git in Project Folder

Open Git Bash:

cd "C:/Users/YourName/eclipse-workspace/MavenJavaProject"
git init
git add .
git commit -m "Initial Maven project"

Step 3: Create Empty Repo on GitHub

On GitHub:

Click New Repository

Name: MavenJavaProject

Do NOT add README or .gitignore

Copy repo URL:

https://github.com/YourUser/MavenJavaProject.git

Step 4: Connect Local Repo to GitHub
git branch -M main
git remote add origin https://github.com/YourUser/MavenJavaProject.git
git push -u origin main


✔ Your Maven project is now on GitHub.

 3. Configure Jenkins Tools

Go to:

Jenkins → Manage Jenkins → Global Tool Configuration

✔ JDK
Name: JDK17
JAVA_HOME: C:\Program Files\Java\jdk-17
(Install automatically → OFF)

✔ Git
Name: git
Path: C:\Program Files\Git\bin\git.exe
(Install automatically → OFF)

✔ Maven
Name: MAVEN_HOME
Install automatically: ✔
Version: Maven 3.9.11 (recommended)


Click Save.

 4. Create Jenkins Freestyle Project

From Jenkins dashboard:

New Item → Freestyle project
Name: mav-jen
OK

 5. Source Code Management (Git)

Select:

✔ Git

Enter:

Repository URL

https://github.com/YourUser/MavenJavaProject.git


Branch to build

*/main

 6. Build Environment

Enable (recommended):

✔ Delete workspace before build starts

 7. Build Step – Maven Build

Click:

Add build step → Invoke top-level Maven targets


Fill:

Maven Version
MAVEN_HOME

Goals
clean install

Advanced → POM
pom.xml


This executes:

mvn clean install


inside Jenkins.

 8. Post-Build Action – Archive Artifact

This makes the JAR visible in Jenkins UI.

Add post-build action → Archive the artifacts


Files to archive:

target/*.jar


Click Save.

 9. Build the Project in Jenkins

Click:

Build Now


Open the latest build (#1, #2, etc.)

Expected console result:

[INFO] BUILD SUCCESS

 10. View the Build Artifact (JAR)

After build, Jenkins shows:

Build Artifacts
  MavenJavaProject-0.0.1-SNAPSHOT.jar


This confirms:

 Maven compiled the project
 JAR created
 Jenkins archived it successfully
 Freestyle CI job fully working