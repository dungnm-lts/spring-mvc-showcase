pipeline {


  agent {
    label 'docker'
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
  post {
      always {
        def attachments = [
            [
              text: 'I find your lack of faith disturbing!',
              fallback: 'Hey, Vader seems to be mad at you.',
              color: '#ff0000'
            ]
          ]
          slackSend(channel: '#devops', attachments: attachments)
      }
   }
}
