pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/annajel/helloworld.git', branch: 'master')
      }
    }

    stage('compile, test, package') {
            withMaven(maven: 'maven'){
            sh label: '', script: 'mvn clean package'
            }
        }

    stage('archival') {
      agent any
      steps {
        archiveArtifacts 'targer/*.war'
      }
    }

  }
  environment {
    test = '1'
  }
}
