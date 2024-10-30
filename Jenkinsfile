pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        SONAR_SCANNER_HOME = '/opt/sonar-scanner'
        PATH = "${JAVA_HOME}/bin:${SONAR_SCANNER_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Verify Java Version') {
            steps {
                sh 'java -version' // Verifies that Java 17 is active
            }
        }

        stage('Scan') {
            steps {
                withSonarQubeEnv('sq2') {
                    sh 'sonar-scanner \
                        -Dsonar.projectKey=DVWA \
                        -Dsonar.sources=.'
                }
            }
        }
    }
}
