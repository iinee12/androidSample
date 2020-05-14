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
        sshPublisher(
            publishers:[
                sshPublisherDesc(configName:'nodeServer',verbose:true,transfers:[
                    sshTransfer(
                        sourceFiles:"abc.tar.gz"
                        // remoteDirectory:"~" //use "~" will made it create a new ~ dir
                    ),
                    sshTransfer(
                        //exec commands
                        execCommand: cmd
                    )
                ])
        ])
      }
    }

  }
}
