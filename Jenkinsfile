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
        registry = 'talgatovan9/artifacts'
        registryCredential = 'dockerhub_id'
      }
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredential)

          {
            dockerImage.push()
          }
        }

      }
    }

  }
}