pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/nayeemcharx/DVWA.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sq2') {
                    // Run SonarScanner in a Docker container with Java 17
                    sh '''
                        docker run --rm \
                            -v "$PWD:/usr/src" \
                            -e SONAR_HOST_URL="$SONAR_HOST_URL" \
                            -e SONAR_LOGIN="$SONAR_AUTH_TOKEN" \
                            sonarsource/sonar-scanner-cli:4.8-java17 \
                            -Dsonar.projectKey=DVWA \
                            -Dsonar.sources=/usr/src \
                            -Dsonar.projectBaseDir=/usr/src \
                            -X
                    '''
                }
            }
        }
    }
}
