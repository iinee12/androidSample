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

    stage('ssh') {
      steps {
        sh 'sh 13.125.253.154'
      }
    }

  }
}