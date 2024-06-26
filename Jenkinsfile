pipeline {
    agent any

    tools {
        // Utiliser la version de Maven installée sur Jenkins
        maven 'maven-3.9.6' // Assurez-vous que ce nom correspond à la configuration de Maven dans Jenkins
    }

    environment {
        // Définir les variables d'environnement nécessaires
        MAVEN_HOME = tool 'maven-3.9.6' // Assurez-vous que ce nom correspond à la configuration de Maven dans Jenkins
        PATH = "${env.MAVEN_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code source depuis le référentiel Git
                checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [], submoduleCfg: [],
                    userRemoteConfigs: [[url: 'https://github.com/HAJARWAFIQ/maven.git']]
                ])
            }
        }

        stage('Build') {
            steps {
                // Nettoyer le projet et compiler le code source avec Maven
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests avec Maven
                bat 'mvn test'
            }
            post {
                // Archiver les résultats des tests et publier les rapports
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Ajouter les étapes de déploiement si nécessaire
                // bat 'mvn deploy'
                echo 'Déploiement effectué'
            }
        }
    }

    post {
        // Notifications et actions à réaliser après le pipeline
        always {
            // Nettoyer le workspace
            cleanWs()
        }
        success {
            echo 'Pipeline terminé avec succès'
        }
        failure {
            echo 'Pipeline échoué'
        }
    }
}
