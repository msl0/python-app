pipeline {
    agent {
        docker {
            image 'python:3.9-alpine'
            label 'node01'
        }
    }
    stages {
          stage('SonarQube Analysis') {
            def scannerHome = tool 'SonarScanner';
            withSonarQubeEnv('sonar') {
              sh "${scannerHome}/bin/sonar-scanner"
            }
          }
        stage('Run') {
            environment { 
                HOME = "${WORKSPACE}"
            }
            steps {
                sh 'pip install -r requirements.txt'
                sh 'python3 -m flask run --host=0.0.0.0 &'
            }
        }
        stage('Test') {
            steps {
                sh 'wget -O- $(hostname):5000'
            }
        }
    }
}
