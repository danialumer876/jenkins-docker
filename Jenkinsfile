pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'sudo docker build -t danialumer876/jenkins-demo:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'sudo docker push danialumer876/jenkins-demo:latest'
      }
    }
  }
  post {
    always {
      sh 'sudo docker logout'
    }
  }
}
