pipeline {
  
  agent {
    docker {
        image 'my-jenkins-slave-mew'
        label 'my-jenkins-slave-new'
        args  '-v /home/ubuntu/cache-vol:/home/jenkins/.m2'
    }
  }
  
  // set max timout for pipeline
  options {
      timeout(time: 60, unit: 'MINUTES')
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
          timeout(time: 30, unit: 'MINUTES') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
        }

    }
  }
}
