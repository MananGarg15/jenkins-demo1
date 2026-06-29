pipeline {
  agent any
  environment {
    DOCKER_CRED = credentials('DockerHub')
  }
  stages {
    stage('fetch-code') {
      steps {
        git branch: 'main', url: 'https://github.com/MananGarg15/jenkins-demo1.git'
      }
    }
    stage('build-image') {
      steps {
        sh 'docker build -t manangarg15/jenkins-app1:${BUILD_NUMBER} .'
      }
    }
    stage('push-image') {
      steps {
        sh ' echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin'
        sh 'docker push manangarg15/jenkins-app1:${BUILD_NUMBER}'
      }
    }
    stage('update-minikube') {
      steps {
        sh 'kubectl set image deployment/pd1 jenkins-app1=manangarg15/jenkins-app1:${BUILD_NUMBER}'
      }
    }
  }
}
