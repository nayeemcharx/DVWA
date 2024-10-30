pipeline {
    agent any

    stages {
        stage('Verify SonarScanner Java Version') {
            steps {
                sh '/opt/sonar-scanner/bin/sonar-scanner --version'
            }
        }
        stage('Clone Repository') {
            steps {
                git 'https://github.com/nayeemcharx/DVWA.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sq2') {
                    sh '''
                        sonar-scanner \
                            -Dsonar.projectKey=DVWA \
                            -Dsonar.sources=. \
                            -X
                    '''
                }
            }
        }
    }
}
