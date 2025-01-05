pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'bash scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh 'bash scripts/test.sh'
      }
    }

    stage('Build docker image') {
      steps {
        sh 'sudo docker build -t cicd .'
      }
    }

    stage('Push docker image') {
      environment {
        DOCKER_PASS = '~zPaVmSwP2N/[{'
        DOCKER_USER = 'talgatovan9'
      }
      steps {
        sh '''sudo docker image tag cicd:latest talgatovan9/artifacts:v2

sudo docker login -u $DOCKER_USER -p $DOCKER_PASS 

sudo docker image push talgatovan9/artifacts:v2'''
      }
    }

  }
}