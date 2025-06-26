pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'localMaven'
    }

    stages {
        stage('Build') {
            steps {
                dir('monprojet') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    dir('monprojet') {
                        sh 'mvn verify sonar:sonar'
                    }
                }
            }
        }
    }
}
