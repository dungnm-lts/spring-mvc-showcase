pipeline {
  agent {
    node {
      label 'master'
    }
  }
  // set max timout for pipeline
  options {
      timeout(time: 3, unit: 'MINUTES')
  }
    tools {
        nodejs 'node'
        maven 'M3'
    }

  stages {
    stage('Build') {
      steps {
              // some block
          sh 'mvn clean install'
      }
    }

    stage('Scan') {
      environment {
        scannerHome = tool 'sonar'
      }
      steps {
          // to know where is sonar url
          // maven not use sonar-project.properties
          // name of sonar in configure system
          withSonarQubeEnv('sonarqube'){
              // some block
              sh 'echo $PATH'
              sh "${scannerHome}/bin/sonar-scanner"
          }

          timeout(time: 1, unit: 'MINUTES') {
              sh 'echo scan timeout'
          }
        }

    }
  }
}
