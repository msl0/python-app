pipeline {
    agent {
        docker {
            image 'python:3.9-alpine'
            label 'node01'
        }
    }

    stages {
        tools {
            'hudson.plugins.sonar.SonarRunnerInstallation' 'SonarScanner'
        }
        stage('Run') {
            environment { 
                HOME = "${WORKSPACE}"
            }
            steps {
                sh 'pip install -r requirements.txt'
                sh 'python3 -m flask run --host=0.0.0.0 &'
                sh 'ls'
                withSonarQubeEnv('sonar') {
                    
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
