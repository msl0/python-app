pipeline {
    agent {
        docker {
            image 'python:3.9-alpine'
            label 'node01'
        }
    }

    stages {
        stage('Run') {
            tools {
                'hudson.plugins.sonar.SonarRunnerInstallation' 'SonarScanner'
            }
            environment { 
                HOME = "${WORKSPACE}"
                scannerHome = tool 'SonarScanner'
            }
            steps {
                sh 'pwd'
                sh 'pip install -r requirements.txt'
                sh 'python3 -m flask run --host=0.0.0.0 &'
                sh 'ls'
                sh 'printenv'
                withSonarQubeEnv('sonar') {
                    sh 'printenv'
                    sh 'ls'
                    sh 'pwd'
                    sh "ls ${scannerHome}"
                    sh "${scannerHome}/bin/sonar-scanner"
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
