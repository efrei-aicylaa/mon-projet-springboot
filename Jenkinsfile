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
                            -Dsonar.login=squ_6c9fe4729fab713e2b1b1a17ac2e18473743a385
                        '''
                    }
                }
            }
        }
    }
}
