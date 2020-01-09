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
          sh 'mvn clean install'
        }
      }
    }
    stage('Scan') {
      steps {
        withMaven(maven: 'M3') {
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
