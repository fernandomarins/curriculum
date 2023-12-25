pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/fernandomarins/curriculum', branch: 'dev')
      }
    }

    stage('Log') {
      parallel {
        stage('Log') {
          steps {
            sh 'ls -la'
          }
        }

        stage('Front-End Unit Tests') {
          steps {
            sh 'npm i && npm run test'
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f Dockerfile .'
      }
    }

    stage('Log in Docker') {
      environment {
        DOCKERHUB_USER = ''
        DOCKERHUB_PASSWORD = ''
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

  }
}