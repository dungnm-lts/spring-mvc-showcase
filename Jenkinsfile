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
              sh 'mvn sonar:sonar -Dsonar.projectKey=spring-mvc-showcase -Dsonar.projectName=spring-mvc-showcase -Dsonar.projectVersion=1.0 -Dsonar.sources=src -Dsonar.tests=src -Dsonar.language=java -Dsonar.java.binaries=./target/classes -Dsonar.log.level=DEBUG -Dsonar.verbose=true -Dsonar.sourceEncoding=UTF-8'
          }
        }
      }
    }
  }
}
