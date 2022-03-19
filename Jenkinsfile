pipeline {
  agent {
    node {
      label 'node01'
    }

  }
  stages {
    stage('Building our image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }

  }
  environment {
    registry = 'user/repo'
    registryCredential = 'dockerhub_id'
    dockerImage = ''
  }
}