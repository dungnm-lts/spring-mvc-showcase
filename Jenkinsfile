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
        script {
          COMMITTER_NAME = sh (
               script: 'git log --format="%an" | head -1',
               returnStdout: true
           ).trim()
          COMMITTER_DATE = sh (
               script: 'git log --format="%aD" | head -1',
               returnStdout: true
            ).trim()
          MESSAGE = sh (
            script: "git log --format=%B -n 1 ${env.GIT_COMMIT}",
            returnStdout: true
            ).trim()
        }
        slackSend (color: "#E44A29", message: "Build Started - git commit: ${env.GIT_COMMIT} --- name: ${COMMITTER_NAME} --- date: ${COMMITTER_DATE} --- git url: ${env.GIT_URL} --- message: ${MESSAGE} --- job name: ${env.JOB_NAME} --- build num: ${env.BUILD_NUMBER} --- build url: (<${env.BUILD_URL}|Open>)")
      }
   }
}
