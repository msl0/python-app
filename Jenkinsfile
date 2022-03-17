pipeline {
    agent none
    stages {
        stage('SonarQube Analysis') {
            agent {
                docker {
                    image 'sonarsource/sonar-scanner-cli:latest'
                }
            }
            steps {
              script {
                def scannerHome = tool 'SonarScanner';
                withSonarQubeEnv('sonar') {
                  sh 'sonar-scanner'
                }
              }
            }
        }
        stage('Run') {
            agent {
                docker {
                    image 'python:3.9-alpine'
                    label 'node01'
                }
            }
            environment { 
                HOME = "${WORKSPACE}"
            }
            steps {
                sh 'pip install -r requirements.txt'
                sh 'python3 -m flask run --host=0.0.0.0 &'
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'python:3.9-alpine'
                    label 'node01'
                }
            }
            steps {
                sh 'wget -O- $(hostname):5000'
            }
        }
    }
}
