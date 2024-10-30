pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        PATH = "${JAVA_HOME}/bin:/opt/sonar-scanner/bin:${env.PATH}"
    }

    stages {
        stage('Verify Java Version') {
            steps {
                sh 'java -version'
                sh 'which sonar-scanner'
            }
        }
        stage('Scan') {
            steps {
                withSonarQubeEnv('sq2') {
                    sh 'sonar-scanner \
                        -Dsonar.projectKey=DVWA \
                        -Dsonar.sources=. \
                        -X'
                }
            }
        }
    }
}
