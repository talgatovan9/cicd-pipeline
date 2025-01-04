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
        DOCKER_REGISTRY = 'https://registry.hub.docker.com'
        DOCKER_CREDENTIALS_ID = 'dockerhub_id'
        DOCKER_IMAGE = 'talgatovan9/cicd-test'
      }
      steps {
        sh '''docker.withRegistry(DOCKER_REGISTRY, DOCKER_CREDENTIALS_ID) {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }'''
          script {
            docker.withRegistry(DOCKER_REGISTRY, DOCKER_CREDENTIALS_ID) {
              app.push("${env.BUILD_NUMBER}")
              app.push("latest")
            }
          }

        }
      }

    }
  }