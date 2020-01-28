pipeline {
  environment {
    registry           = "zaap59/spinnaker-sampleapp"
    registryCredential = "dockerhub"
    dockerImage        = ''
    tag                = sh(returnStdout: true, script: "git tag --contains | head -1").trim()
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
          sh "docker build -t ${registry}:${tag} ."
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            sh "docker push ${registry}:${tag}"
          }
        }
      }
    }
  }
}
