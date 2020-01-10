pipeline {
  agent {
    node {
      label 'master'
    }

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
        // name of global tool configuration
        def node = 'node'
        withMaven(maven: 'M3') {

          // to know where is sonar url
          // maven not use sonar-project.properties
          // name of sonar in configure system
          withSonarQubeEnv('sonarqube'){
              // some block
              sh 'echo $PATH'
              sh 'mvn sonar:sonar -Dsonar.nodejs.executable=${tool node}/bin/node'
          }

        }
      }
    }
  }
}
