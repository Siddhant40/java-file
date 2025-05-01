**Jenkins Parallel Java Program Execution Pipeline**

📖 Overview
This project demonstrates implementing parallel execution of Java programs using Jenkins Pipelines. The pipeline is designed to:

Use a Docker container for Java compilation and execution

Compile and run two Java programs in parallel

Archive the compiled .class files

Clean up the Jenkins workspace post-execution


🛠️ Jenkins Pipeline Workflow

✅ Step 1: Setting Up a Containerized Environment
To ensure a proper and isolated environment for compiling Java programs, a Docker container with a pre-configured Java image was used.

Steps Performed:

Installed and ensured Docker was running on my system.

Installed the Docker Pipeline plugin in Jenkins.

Created a new Pipeline Job in Jenkins.

agent1 is a Jenkins agent pre-configured to use Docker as its environment, enabling containerized builds automatically without needing to explicitly declare a docker block in each pipeline.

Executed the pipeline and verified that Jenkins successfully set up the containerized environment.

📸 Screenshot 1: Showing the successful container setup.
![image](https://github.com/user-attachments/assets/e6649be1-efc8-4753-be1c-4c0159df88ba)


✅ Step 2: Created a New Jenkins Project
Project Name: Parallel

Configured the pipeline with parallel execution stages

✅ Step 3: Jenkins Pipeline Code
groovy
Copy
Edit
pipeline {
    agent { label 'agent1' }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Siddhant40/java-file.git'
            }
        }

        stage('Run Java Files in Parallel') {
            parallel {
                stage('Run Main1.java File') {
                    steps {
                        script {
                            sh 'javac Main1.java && java Main1'
                        }
                    }
                }
                stage('Run Main2.java File') {
                    steps {
                        script {
                            sh 'javac Main2.java && java Main2'
                        }
                    }
                }
            }
        }

        stage('Archive Compiled Java Class Files') {
            steps {
                archiveArtifacts artifacts: '*.class', fingerprint: true
                echo '📦 Java class files archived successfully!'
            }
        }

        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                echo '🧹 Workspace cleaned up successfully!'
            }
        }
    }
    }
  
✅ Step 4: Parallel Execution Verification
Executed the pipeline and verified both Java programs were compiled and executed in parallel.

📸 Screenshot 3: Parallel execution of Main1.java and Main2.java
![image](https://github.com/user-attachments/assets/bdd41722-3c85-4024-af09-1adcd71bd992)


📸 Screenshot 4: Successful compilation and execution confirmation
![image](https://github.com/user-attachments/assets/76b582e0-afda-4efc-a01a-d08c94d63ff1)


✅ Step 5: Archiving Artifacts
Added archiveArtifacts step to store compiled .class files.

📸 Screenshot 5: Archived .class files visible and downloadable in Jenkins artifacts section.
![image](https://github.com/user-attachments/assets/db40601d-d7cf-4411-b717-a63dd8279269)


✅ Step 6: Cleaning Up the Workspace
Implemented cleanWs() step to clean up the workspace after pipeline execution.

📸 Screenshot 6: Workspace cleaned successfully post-execution.
![image](https://github.com/user-attachments/assets/a19bf882-8418-490b-b234-a05e9c46ee36)


📌 Conclusion
This project illustrates how Jenkins Pipelines can be used to:

Perform parallel execution

Archive build artifacts

Maintain a clean and efficient build environment



