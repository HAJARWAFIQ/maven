pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clean the directory
                bat 'del /S /Q *'

                // Checkout the Git repository
                bat 'git clone https://github.com/simoks/java-maven.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"

                    // Navigate to the directory containing the Maven project
                    dir('java-maven/maven') {
                        // Run Maven commands
                        bat 'mvn clean test package'

                        // Run the packaged JAR file
                        bat 'java -jar target\\maven-0.0.1-SNAPSHOT.jar'
                    }
                }
            }
        }
    }
}
