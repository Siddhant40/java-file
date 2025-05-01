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
