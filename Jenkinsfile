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
        stage('Export SonarQube Issues') {
            steps {
                withSonarQubeEnv('sq2') {
                    sh '''
                        curl -u "$SONAR_AUTH_TOKEN:" \
                        "$SONAR_HOST_URL/api/issues/search?componentKeys=DVWA&resolved=false&ps=500" \
                        -o sonarqube_issues.json
                    '''
                }
            }
        }
        stage('Import to DefectDojo') {
            steps {
                withCredentials([string(credentialsId: 'defectdojo-api-token', variable: 'DEFECTDOJO_API_TOKEN')]) {
                    script {
                        def defectdojoServer = 'http://your-defectdojo-server'
                        def engagementId = 'your_engagement_id'

                        // Import SonarQube issues into DefectDojo via API
                        sh """
                            curl -X POST -H "Authorization: Token $DEFECTDOJO_API_TOKEN" \
                            -F 'file=@sonarqube_issues.json' \
                            -F 'scan_type=SonarQube API Import' \
                            -F 'engagement=${engagementId}' \
                            '${defectdojoServer}/api/v2/import-scan/'
                        """
                    }
                }
            }
        }
    }
}
