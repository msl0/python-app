pipeline {
    agent {
        docker {
            image 'python:3.9-alpine'
            label 'node01'
        }
    }
    stages {
        stage('Run') {
            environment { 
                HOME = "${WORKSPACE}"
            }
            steps {
                sh 'pip install -r requirements.txt'
                sh 'python3 -m flask run --host=0.0.0.0 &'
                sh 'wget $(hostname):5000'
            }
        }
    }
}
