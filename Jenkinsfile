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
      }
    }
  }
}