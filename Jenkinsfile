pipeline {
  agent any
  stages {
    stage('Codigo Fuente') {
      steps {
        parallel(
          "Hola": {
            echo 'Hola devops!'
            
          },
          "GitPull": {
            git 'https://github.com/andreinaromero/sampleapp.git'
            
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
    stage('Analisis Estatico') {
      steps {
        sh 'mvn -DeskipTests checkstyle:checkstyle pmd:pmd findbugs:findbugs'
        checkstyle(pattern: 'target/checkstyle-result.xml')
        pmd(pattern: 'target/pmd.xml')
        findbugs(pattern: 'target/findbugsXml.xml')
      }
    }
    stage('Publicar artefacto') {
      steps {
        sh 'mvn clean package -DskipTests'
        archiveArtifacts 'target/webapp-*.jar'
      }
    }
  }
}