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
    stage('IntegrationTest') {
      steps {
        sh 'mvn verify -DskipUTs'
        junit 'target/failsafe-reports/*.xml'
      }
    }
    stage('An�lisis Est�tico') {
      steps {
        sh 'mvn -DeskipTests checkstyle:checkstyle pmd:pmd findbugs:findbugs'
      }
    }
  }
}