pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64' // Path to Java 17
        SONAR_SCANNER_HOME = '/opt/sonar-scanner' // Path to sonar-scanner
        PATH = "${JAVA_HOME}/bin:${SONAR_SCANNER_HOME}/bin:${env.PATH}" // Add Java 17 and sonar-scanner to PATH
    }

    stages {
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
