pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
      }
    }
    stage('test') {
      steps {
        sh 'mvn clean cobertura:cobertura test'
      }
    }
    stage('report') {
      parallel {
        stage('report') {
          steps {
            junit 'target/surefire-reports/*.xml'
          }
        }
        stage('coverage') {
          steps {
            cobertura(coberturaReportFile: 'target/site/cobertura/coverage.xml')
          }
        }
      }
    }
    stage('package') {
      steps {
        sh 'mvn package'
      }
    }
    stage('archive') {
      steps {
        archiveArtifacts(artifacts: 'target/spring-boot-sample-data-rest-0.1.0.jar', allowEmptyArchive: true)
      }
    }
    stage('deploy') {
      steps {
        sh 'make deploy-default'
      }
    }
  }
  post {
    always {
      echo 'I will always say Hello again!'

    }

    success {
      echo 'success!'

    }

    failure {
      echo 'failure!'

    }

  }
}