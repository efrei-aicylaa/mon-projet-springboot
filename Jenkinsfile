pipeline {
  agent any

  tools {
    jdk 'Java17'
    maven 'localMaven'
  }

  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('MySonarQube') {
          sh 'mvn sonar:sonar'
        }
      }
    }
  }
}
