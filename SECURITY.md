groovy
pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t poormansbank .'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run -p 8080:8080 poormansbank'
      }
    }
    stage('Deploy') {
      steps {
        sh 'jira deploy --cluster poormansbank --service poormansbank'
      }
    }
  }
}
                        
