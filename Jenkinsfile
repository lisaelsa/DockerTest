pipeline {
  agent { label 'SnowflakeBDI1' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('DockerToken')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t lisaelsa/go-app .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push lisaelsa/go-app'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
