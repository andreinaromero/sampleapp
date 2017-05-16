pipeline {
  agent any
  stages {
    stage('Hola') {
      steps {
        parallel(
          "Hola": {
            echo 'Hola devops!'
            
          },
          "GitPull": {
            git 'https://github.com/adrianmoya/sampleapp.git'
            
          }
        )
      }
    }
    stage('UnitTest') {
      steps {
        sh 'mvn clean test'
        junit 'target/surefire-reports/*.xml'
        catchError() {
          junit 'target/surefire-reports/*.xml'
        }
        
      }
    }
    stage('AceptanceTest') {
      steps {
        sh 'mvn verify -DskipUTs'
        junit 'target/failsafe-reports/*.xml'
      }
    }
  }
}