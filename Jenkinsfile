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
        sh 'sudo docker build -t cicd-test .'
      }
    }

    stage('Push docker image') {
      environment {
        DOCKER_PASS = '~zPaVmSwP2N/[{'
        DOCKER_USER = 'talgatovan9'
      }
      steps {
        sh '''sudo docker image tag cicd-test:latest registry.hub.docker.com/talgatovan9/cicd-test/cicd-test:latest

docker login -u $DOCKER_USER -p $DOCKER_PASS 

sudo docker image push registry.hub.docker.com/talgatovan9/cicd-test/cicd-test:latest'''
      }
    }

  }
}