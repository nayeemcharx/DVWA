pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = '/opt/sonar-scanner'
    }

    stages {
        stage('Verify Java Version') {
            steps {
                sh 'java -version' // Verify Java 17
            }
        }

        stage('Scan') {
            steps {
                withSonarQubeEnv('sq2') {
                    sh '${SONAR_SCANNER_HOME}/bin/sonar-scanner-java17 \
                        -Dsonar.projectKey=DVWA \
                        -Dsonar.sources=.'
                }
            }
        }
    }
}
