pipeline {
  agent any

  tools {
    jdk 'Java17'        // ou le nom exact donné dans Jenkins
    maven 'localMaven'  // idem ici
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
