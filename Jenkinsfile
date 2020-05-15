pipeline {
  agent any
  stages {
    stage('Auth') {
      steps {
        sh 'chmod +x gradlew'
      }
    }

    stage('build') {
      steps {
        sh './gradlew --no-daemon assembleDebug --stacktrace'
      }
    }

    stage('Artifacts') {
      steps {
        archiveArtifacts(artifacts: '*/build/**/*.apk', onlyIfSuccessful: true)
      }
    }


    stage('history') {
      steps {
        httpRequest(url: 'http://13.125.253.154:3000/cicdRequest', acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_JSON', httpMode: 'POST', responseHandle: 'STRING', requestBody: '{"indexNo":${BUILD_ID}, "appVersion":"${EXECUTOR_NUMBER}", "appName":"${JOB_NAME}", "buildUser":"${NODE_NAME}", "appPath":""}')
      }
    }

  }
}
