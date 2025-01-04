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

    stage('Build docker') {
      steps {
        sh 'docker build -t cicd-test'
      }
    }

  }
}