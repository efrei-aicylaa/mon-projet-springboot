pipeline {
    agent any

    tools {
        jdk 'jdk-17'         // Nom défini dans Jenkins > Global Tool Configuration
        maven 'Maven 3.6.3'  // Nom défini pour Maven dans Jenkins
    }

    environment {
        SONARQUBE = 'MySonarQube' // Nom du serveur SonarQube configuré dans Jenkins > SonarQube Servers
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/efrei-aicylaa/mon-projet-springboot.git'
            }
        }

        stage('Build with Maven') {
            steps {
                dir('monprojet') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('monprojet') {
                    withSonarQubeEnv("${SONARQUBE}") {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
    }
}
