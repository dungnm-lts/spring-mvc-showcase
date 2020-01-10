pipeline {
  agent {
    node {
      label 'master'
    }
  }

    tools {
        nodejs 'node'
        maven 'M3'
        sonar 'sonar'
    }

  stages {
    stage('Build') {
      steps {
              // some block
          sh 'mvn clean install -DskipTests'
      }
    }

    stage('Scan') {
      steps {
          // to know where is sonar url
          // maven not use sonar-project.properties
          // name of sonar in configure system
          withSonarQubeEnv('sonarqube'){
              // some block
              sh 'echo $PATH'
              sh "sonar-scanner"
          }
        }

    }
  }
}
