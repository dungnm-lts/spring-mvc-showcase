pipeline {
  agent {
    node {
      label 'master'
    }

  }
tools {
  // name of tool and
  // name of global tool configuration
  nodejs 'node'
}

  stages {
    stage('Build') {
      steps {
        withMaven(maven: 'M3') {
              // some block
          sh 'mvn clean install -DskipTests'
        }
      }
    }
    stage('Scan') {
      steps {

        withMaven(maven: 'M3') {

          // to know where is sonar url
          // maven not use sonar-project.properties
          // name of sonar in configure system
          withSonarQubeEnv('sonarqube'){
              // some block
              sh 'echo $PATH'
              sh 'mvn sonar:sonar -Dsonar.nodejs.executable=node'
          }

        }
      }
    }
  }
}
