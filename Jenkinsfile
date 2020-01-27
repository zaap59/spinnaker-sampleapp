pipeline {
  environment {
    registry = "zaap59/spinnaker-sampleapp"
    registryCredential = "dockerhub"
    dockerImage = ''
  }
  agent {
    kubernetes {
        label 'jenkins-jenkins-slave'
    }
  }
  stages {
    stage('Building image') {
      steps{
        script {
          sh "docker build -t ${registry}:${BUILD_NUMBER} ."
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            sh "docker push ${registry}:${BUILD_NUMBER}"
          }
        }
      }
    }
  }
}