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


 
