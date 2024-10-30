pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64' // Explicitly use Java 17
        SONAR_SCANNER_HOME = '/opt/sonar-scanner'
        PATH = "${JAVA_HOME}/bin:${SONAR_SCANNER_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Verify Java Version') {
            steps {
                sh 'java -version' // Ensures Java 17 is active
                sh '${SONAR_SCANNER_HOME}/bin/sonar-scanner --version' // Verifies sonar-scanner path
            }
        }

        stage('Scan') {
            steps {
                withSonarQubeEnv('sq2') {
                    sh 'JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64 ${SONAR_SCANNER_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKey=DVWA \
                        -Dsonar.sources=.'
                }
            }
        }
    }
}
