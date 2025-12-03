Maven Java Project – Creation, Execution, and GitHub Deployment

This guide explains how to:

Create a Maven Java Project in Eclipse

Add and run a Java class

Commit the entire project

Push it to GitHub

Everything is written step-by-step with zero confusion.

 1. Create a New Maven Java Project in Eclipse
 Step 1: Open Eclipse

Go to:

File → New → Maven Project

 Step 2: Select Project Type

Check:

 Create a simple project (skip archetype selection)
Click Next.

 Step 3: Enter Maven Details

Fill these:

Field	Value
Group Id	com.example
Artifact Id	MavenJavaProject
Packaging	jar
Version	Default

Click Finish.

Eclipse creates the standard Maven structure:

MavenJavaProject/
 ├── src/main/java
 ├── src/test/java
 ├── pom.xml

 2. Create Java Class with main()
Step 1: Create a Package

Right-click:

src/main/java → New → Package


Enter:

com.example.app

Step 2: Create a Java Class

Right-click on the package:

com.example.app → New → Class


In the dialog:

Name: MainApp

Tick ✔️ public static void main(String[] args)

Click Finish.

Step 3: Add Code

Eclipse auto-generates the file:

package com.example.app;

public class MainApp {
    public static void main(String[] args) {
        System.out.println("Hello from Maven Java Project!");
    }
}

 3. Run the Project in Eclipse

Right-click on MainApp.java →

Run As → Java Application


Console output should show:

Hello from Maven Java Project!

 4. Find the Project Folder Location (Required for GitHub Push)

Right-click MavenJavaProject → Properties

Under Resource, note the path:

Example:

C:\Users\YourName\eclipse-workspace\MavenJavaProject


You will use this path in Git Bash.

 5. Create a New Repository on GitHub

Go to github.com

Click New Repository

Enter name: MavenJavaProject

Do NOT add:

README

.gitignore

License

Click Create Repository

Copy the repository HTTPS URL:

https://github.com/YourName/MavenJavaProject.git

 6. Push Project to GitHub Using Git Bash
Step 1: Open Git Bash at your project location
cd "C:/Users/YourName/eclipse-workspace/MavenJavaProject"

Step 2: Initialize Git
git init

Step 3: Add all project files
git add .

Step 4: Commit
git commit -m "Initial Maven Java project"

Step 5: Add GitHub remote
git branch -M main
git remote add origin https://github.com/YourName/MavenJavaProject.git

Step 6: Push the project
git push -u origin main


Your Maven Java project is now uploaded to GitHub.

 7. Project Structure After Push
MavenJavaProject/
 ├── src
 │   ├── main
 │   │   └── java
 │   │       └── com/example/app/MainApp.java
 │   ├── test
 │   └── resources
 ├── target/
 └── pom.xml