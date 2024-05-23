pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clean the directory (Windows)
                bat "del /s /q *"
                // Checkout the Git repository
                bat "git clone https://github.com/simoks/java-maven.git"
            }
        }
        stage('Build') {
            steps {
                // Here, we can run Maven commands
                script {
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"
                   
                    // Navigate to the directory containing the Maven project
                    dir('java-maven/maven') {
                        // Run Maven commands
                        bat 'mvn clean test package'
                        bat "java -jar target/maven-0.0.1-SNAPSHOT.jar"
                    }
                }
            }
        }
    }
}
