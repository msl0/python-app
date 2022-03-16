pipeline {
    agent {
        docker {
            image 'python:3.9-alpine'
            label 'node01'
        }
    }
    tools {
        'hudson.plugins.sonar.SonarRunnerInstallation' 'SonarScanner'
    }
    stages {
        stage('Run') {
            environment { 
                HOME = "${WORKSPACE}"
            }
            steps {
                sh 'pip install -r requirements.txt'
                sh 'python3 -m flask run --host=0.0.0.0 &'
                sh 'ls'
                withSonarQubeEnv('sonar') {
                    //sonar-scanner
                }
            }
        }
        stage('Test') {
            steps {
                sh 'wget -O- $(hostname):5000'
            }
        }
    }
}
