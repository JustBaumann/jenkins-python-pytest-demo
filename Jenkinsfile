pipeline {
  agent {
    docker { image 'python:3.11' }
  }
  stages {
    stage('Install dependencies') {
      steps {
        sh 'python --version'
        sh 'pip install -r requirements.txt'
      }
    }
    stage('Run tests') {
      steps {
        sh 'pytest --junitxml=report.xml'
      }
    }
    stage('Publish Report') {
      steps {
        junit 'report.xml'
      }
    }
  }
}
