pipeline {
    agent any

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
