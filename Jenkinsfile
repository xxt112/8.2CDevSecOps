pipeline {
    agent any
    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN') // 你在 Jenkins 里设置的 token ID
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/xxt112/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                sh '''
                set -x
                echo ">>> Current directory:"
                pwd
                echo ">>> Contents:"
                ls -alh

                echo ">>> Cleaning"
                rm -rf sonar-scanner-5.0.1.3006-linux sonar-scanner.zip

                echo ">>> Downloading"
                curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip

                echo ">>> Unzipping"
                unzip -q sonar-scanner.zip

                echo ">>> Granting permissions"
                chmod +x sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner

                echo ">>> Running scanner"
                sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner \
                    -Dsonar.projectKey=xxt112 \
                    -Dsonar.organization=xxt112 \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=$SONAR_TOKEN
                '''
            }
        }
    }
}
