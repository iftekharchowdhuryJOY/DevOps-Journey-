# JENKINS 101
Imagine you and your friends are building a massive LEGO castle.

**The Old Way (No CI)**: Everyone goes into separate rooms and builds a big section of the castle independently. After a whole week, you all bring your giant sections together. But when you try to connect them, nothing fits! The doors don't align, the towers are different styles, and it's a huge mess to fix.

**The New Way (With CI)**: This is Continuous Integration. Instead of building huge sections alone, every time a friend finishes a tiny piece (like a single wall or a small window), they immediately add it to the main castle. Everyone can see the changes right away. If a piece doesn't fit, you discover the problem instantly and fix it when it's still a small, easy issue.

In software development, that "castle" is the application's code, and the "friends" are developers. Continuous Integration means developers merge their code changes into a central repository frequently. Each time they do, an automated process builds the software and runs tests to make sure the new code doesn't break anything.

Continuous Delivery/Deployment (CD) is the next step. Once the tests pass, the changes are automatically prepared and delivered, ready to be released to users.

## So, why is this so important? 
It helps teams catch bugs early, improve collaboration, and release new features to users much faster and more reliably.

# Jenkins
 **Jenkins isn't the code repository (like GitHub) or the testing tool itself. It's the automation engine that orchestrates the entire workflow from code to release. It’s the brain of the operation!**

<p>
  The whole automated process kicks off the moment a developer "brings in the new code"—or, in technical terms, when they commit or merge their code changes to a central repository like GitHub. Jenkins constantly watches that repository, and the new code is the signal to start working.
</p>

## Let's install JENKINS

I installed Jenkins for my RHEL distribution. So, I don't know about Windows. 

1. Add the Jenkins Repository. First, you tell your system's package manager (dnf or yum) where to find Jenkins.
```bash
# Add the Jenkins repository
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

# Import the key to verify the repository's authenticity
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
```
2. Install Java (A Prerequisite)
```Bash
# Update your system and install Java 17
sudo dnf upgrade
sudo dnf install fontconfig java-17-openjdk
```
3. Install Jenkins
``` sudo dnf install jenkins ```

4. Start Jenkins
```Bash
# Start the service now
sudo systemctl start jenkins

# Enable it to start on boot
sudo systemctl enable jenkins

# You can check its status to make sure it's running
sudo systemctl status jenkins
```
5. Post-installation setup wizard
```Bash
- http://localhost:8080
- sudo cat /var/lib/jenkins/secrets/initialAdminPassword will print the password to the console.

```
6. Customizing Jenkins with plugins
If you are unsure what plugins you need, choose Install suggested plugins.

Jenkins is a powerful orchestrator, but it doesn't know how to do everything itself. It needs plugins to handle specific tasks, like:

- Talking to your code repository (the Git plugin)
- Building your code with specific tools (like Maven or Gradle plugins)
- Sending you a notification on Slack or via email

Now, after those plugins finish installing, Jenkins finally takes you to that main dashboard. It's empty, but ready for instructions.
# My First Jenkins Job
1. Start from the Dashboard: From the main Jenkins page, you clicked "+ New Item" to begin creating a new task.
2. Choose Your Project Type: You gave your job a name (Hello-World) and, most importantly, you selected a Freestyle project. We chose this because it's a great starting point that lets you configure steps visually using dropdown menus.
3. Configure the "What" and "How": This was the most important part. On the configuration screen:
4. Source Code Management: You skipped this section entirely (leaving it as "None") because our simple job didn't need to pull code from a place like GitHub.
5. Build Steps: You told Jenkins what to do. You clicked "Add build step" and chose "Execute shell". In the command box, you gave it the simple echo command to print a message. This was the actual "work" the job had to perform.
6. Save and Run: You clicked "Save" to store the job's configuration. Then, back on the job's main page, you clicked "Build Now" to manually kick it off.
7. Check the Results: You confirmed the job's success in two ways:
8. Build History: You saw the build number with a blue dot next to it, which means "SUCCESS".
9. Console Output: You clicked into the build and viewed the Console Output. This is the most critical step for debugging, as it showed you the exact log of what Jenkins did, including the "Hello from Jenkins!" message you told it to print.

## Understanding Jenkins Pipelines
A Pipeline, however, is like writing down the entire, detailed recipe in a text file. Instead of clicking buttons, you describe your entire build, test, and deployment process in code.
This approach is called "Pipeline as Code."

# Why You Need a Jenkinsfile (The Big Advantages)
Imagine your company has 20 different software projects.

1. With Freestyle jobs: You would have to manually create and configure 20 different jobs in the Jenkins UI. If you need to update them all, you have to edit all 20 jobs by hand. It's slow and prone to errors.
2. With a Jenkinsfile, You can create one master Jenkinsfile template. All 20 projects can just use that same file. If you need to make an update, you change it in one place.
Here are the key benefits of "Pipeline as Code":

3. It's Version Controlled: The Jenkinsfile is saved in GitHub with your code. You can see who changed the build process and when. You can revert to an old version if a change breaks things. With Freestyle, the configuration is just "somewhere" in Jenkins, and it's hard to track changes.
4. It's More Durable: If your Jenkins server completely crashes and you lose everything, your Freestyle job configurations are gone forever. But with a Jenkinsfile, the "recipe" for your build is safely stored in GitHub. You can set up a new Jenkins server and point it to your code, and you're back in business instantly.
5. It's Sharable and Reusable: As in the example above, you can share and reuse pipelines across many projects, which is much more efficient.
6. It Allows for Code Review: A change to the build process can be reviewed by your teammates in a Pull Request, just like any other code. This prevents one person from making a change in the UI that could accidentally break the entire project.

# How a Jenkinsfile Works (The Mechanics)
So how does Jenkins actually use this file? It's a two-part process:

1. In your Code Repository (like GitHub): You create a file named Jenkinsfile. You write the steps for your build inside this text file.

2. In Jenkins: You create a new type of job. Instead of "Freestyle project," you choose "Pipeline". The configuration for this job is incredibly simple. Instead of adding lots of build steps, you just do one thing: you go to the "Pipeline" section and tell it, "get your instructions from a Jenkinsfile in my Git repository."

Here is what a very simple Jenkinsfile looks like:

```Groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Hello from a Jenkins Pipeline!'
            }
        }
    }
}
```
- pipeline { ... }: This is the main block that wraps the entire script. Everything must be inside this.

- agent any: This tells Jenkins where to run the job. The agent is the machine or environment that will execute the steps. agent any is the simplest option—it just tells Jenkins to run this on any available machine.

- stages { ... }: This block contains all the different phases of our process. A typical pipeline is broken down into multiple stages.

- stage('...') { ... }: This defines a specific phase of your pipeline. You give it a name, like 'Build', 'Test', or 'Deploy'. These stages show up as separate columns in the Jenkins UI, so you can see where your process succeeded or failed.

- steps { ... }: Inside each stage, the steps block contains the actual commands you want to run.

- echo '...': This is one of those steps! It's the same echo command we used in our Freestyle job.


When Jenkins runs this, it will:

Execute everything inside the stage('Build').
If that succeeds, it will move on and execute everything inside the stage('Test').

```Groovy
pipeline {
    agent any

    stages {
        // Stage 1
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }

        // --- THIS IS THE NEW PART WE ADDED ---
        // Stage 2
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        // ------------------------------------

    }
}

```
# The Power of Plugins
Think of a brand new smartphone. Out of the box, it can make calls, send texts, and browse the internet. It has the basic functions. But its real power comes from the App Store. When you want to navigate somewhere, you install Google Maps. When you want to listen to music, you install Spotify.

Jenkins works exactly the same way:

- Base Jenkins is the smartphone. It knows how to run jobs and orchestrate pipelines.
- Plugins are the apps you install to give Jenkins new powers.
- When you first set up Jenkins, you already did this when you chose "Install suggested plugins". You were installing the "apps" needed for common tasks!
- When you install a plugin, it gives you new commands (or steps) that you can use in your Jenkinsfile.

For example:

- To get code from GitHub, you need the Git Plugin, which gives you a git step.
- To build a Java project with Maven, you need the Maven Plugin, which gives you tools for running Maven commands.
- To send a notification to a Slack channel, you need the Slack Plugin, which gives you a slackSend step.
- So, the steps block in your Jenkinsfile might look like this with plugins:


```Groovy
steps {
    // This 'git' step comes from the Git Plugin
    git 'https://github.com/your-repo/your-project.git'

    // This 'sh' step is a basic command to run a Maven build
    sh './mvnw clean install'
}
```
# Where Jenkins Stores Logs

1. Path: ```bash /var/lib/jenkins/jobs/<JOB_NAME>/builds/<BUILD_NUMBER>/log```
2. Example /var/lib/jenkins/jobs/flask ci-cd/builds/1

# Key Takeaways
1. Logs: Stored in jobs/<JOB>/builds/<NUMBER>/log.
2. Workspace: Temporary directory for code (/workspace/<JOB>).
3. Access: Use UI, CLI, or archiveArtifacts to save logs.


# What Are Test Cases in Jenkins?
Test cases in Jenkins refer to automated checks (usually unit/integration tests) that validate your code works as expected. They are not a Jenkins feature—they’re your own tests (written in frameworks like pytest, JUnit, Jest, etc.) that Jenkins runs and reports on.
# Example Test Cases (Python)
```python
# test_math.py (A simple pytest test file)
def test_add():
    assert 1 + 1 == 2   # Passes

def test_fail():
    assert 2 * 2 == 5   # Fails (intentionally)
```
# How Jenkins Handles Test Cases
Jenkins executes your tests (via sh, bat, or plugins) and records results. Key components:
a) Running Tests
In your Jenkinsfile:
```groovy
stage('Test') {
    steps {
        sh 'pytest test_math.py'  // Runs Python tests
        // OR for Java:
        sh 'mvn test'             // Runs JUnit tests
    }
}
```
# Test Reports
Jenkins collects results from test frameworks:

* JUnit (Java/Kotlin): mvn test generates target/surefire-reports/*.xml.

* pytest (Python): pytest --junitxml=report.xml generates XML reports.

* Jest (JavaScript): jest --ci --reporters=default --reporters=jest-junit.

Configure Jenkins to publish reports:
```groovy
post {
    always {
        junit '**/test-results.xml'  // Publishes test results to Jenkins UI
    }
}
```
# What Does "Test Pass/Fail" Mean in Jenkins?
* Pass: All tests ran successfully (exit code 0 + no failures in reports).
* Fail: At least one test failed (exit code ≠0 or XML report shows failures).

# Where to See Results
* Console Output: Raw logs of test execution.
* Test Results Trend: Graph of pass/fail over time (Jenkins UI → Job → "Test Result Trend").
* Detailed Reports: Click individual builds to see which tests failed.

**No more manual testing:** Jenkins runs tests on every commit.
**Catch bugs early**: Before they reach production.
**Team transparency**: Everyone sees test results in Jenkins.










 
