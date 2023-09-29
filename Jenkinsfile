pipeline {
  agent { label 'docker-slave' }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t aks0207/jenkins-docker-hub .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push aks0207/jenkins-docker-hub'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
