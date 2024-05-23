pipeline {
    agent any

    stages {
        stage('Prepare Environment') {
            steps {
                script {
                    // Clean the workspace safely
                    deleteDir()
                }
            }
        }
        stage('Checkout') {
            steps {
                // Checkout the Git repository
                git url: 'https://github.com/HAJARWAFIQ/maven.git', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                // Here, we can run Maven commands
                script {
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"
                   
                    // Navigate to the directory containing the Maven project
                    dir('maven') {
                        // Run Maven commands
                        bat 'mvn clean test package'
                        bat "java -jar target/maven-0.0.1-SNAPSHOT.jar"
                    }
                }
            }
        }
    }
}
