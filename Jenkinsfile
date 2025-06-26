pipeline {
    agent any

    tools {
        jdk 'Java17'          // correspond à ton JDK installé automatiquement
        maven 'localMaven'         // correspond au Maven défini à /usr/share/maven
    }

    environment {
        JAVA_HOME = "/opt/java/openjdk"                 // validé dans ton conteneur
        PATH = "${JAVA_HOME}/bin:${PATH}"               // pour rendre Java visible
        SONARQUBE = 'SonarQube'                         // le nom défini dans Jenkins > SonarQube Servers
    }

    stages {
        stage('Clonage Git') {
            steps {
                checkout scm
            }
        }

        stage('Build Maven') {
            steps {
                dir('monprojet') {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Analyse SonarQube') {
            steps {
                dir('monprojet') {
                    withSonarQubeEnv("${SONARQUBE}") {
                        sh '''
                            mvn verify sonar:sonar \
                            -Dsonar.projectKey=AppSpringboot \
                            -Dsonar.host.url=http://172.16.100.9:9000 \
                            -Dsonar.login=sqp_5d11f687cd5f2e53eaf08739b7c01d6005a90b03
                        '''
                    }
                }
            }
        }
    }
}
