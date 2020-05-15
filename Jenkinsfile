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
    
    stage('print') {
      steps {
        echo "${BUILD_ID}"
      }
    }
    
    stage('history') {
      steps {
        httpRequest(url: 'http://13.125.253.154:3000/cicdRequest', acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_JSON', httpMode: 'POST', responseHandle: 'STRING', requestBody: '{"indexNo":1, "appVersion":"2321", "appName":"11", "buildUser":"34", "appPath":"44"}')
      }
    }

  }
}
