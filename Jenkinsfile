pipeline {
  agent any
  stages {
    stage('checkout') {
        git 'https://github.com/annajel/helloworld.git'
        }
        
        stage('compile, test, package') {
            withMaven(maven: 'maven'){
            sh label: '', script: 'mvn clean package'
            }
        }
        
        stage('archival') {
            archiveArtifacts 'target/*.war'
        }
  }
  environment {
    test = '1'
  }
}
