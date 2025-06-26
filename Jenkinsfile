pipeline {
    agent any

    tools {
        jdk 'Java17'           // doit correspondre au nom défini dans Global Tool Configuration
        maven 'localMaven'    // idem pour Maven
    }

    environment {
        SONARQUBE = 'SonarQube' // nom du serveur SonarQube défini dans Jenkins (Manage Jenkins > Configure System)
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
        PATH = "${JAVA_HOME}/bin:${PATH}"
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
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.login=sqp_5d11f687cd5f2e53eaf08739b7c01d60050a9b03
                        '''
                    }
                }
            }
        }
    }
}
