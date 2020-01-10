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
        withMaven(maven: 'M3') {
          withEnv(["PATH+NODE=${tool 'node'}/bin]) {
          // to know where is sonar url
          // maven not use sonar-project.properties
          withSonarQubeEnv('sonarqube'){
              // some block
              sh 'mvn sonar:sonar'
          }
                   }
        }
      }
    }
  }
}
