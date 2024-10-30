pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64' // Set to JDK 17
        PATH = "${JAVA_HOME}/bin:${env.PATH}" // Add JDK 17 to PATH
    }

    stages {
        stage('Prepare Environment') {
            steps {
                // Install sonar-scanner and Java JDK 17
                sh '''
                    apt-get update && \
                    apt-get install -y curl unzip openjdk-17-jdk && \
                    curl -o sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-linux.zip && \
                    unzip sonar-scanner.zip -d /opt && \
                    mv /opt/sonar-scanner-* /opt/sonar-scanner && \
                    rm sonar-scanner.zip
                '''
                // Update PATH for sonar-scanner
                script {
                    env.SONAR_SCANNER_HOME = '/opt/sonar-scanner'
                    env.PATH = "${env.SONAR_SCANNER_HOME}/bin:${env.PATH}"
                }
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
