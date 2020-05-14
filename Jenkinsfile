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

    stage('SSH') {
      steps {
        sshPublisher(
          alwaysPublishFromMaster: true,
        [
    sshPublisherDesc(
     configName: "${env.SSH_CONFIG_NAME}",
     verbose: true,
     transfers: [
      sshTransfer(
       sourceFiles: "${path_to_file}/${file_name}, ${path_to_file}/${file_name}",
       removePrefix: "${path_to_file}",
       remoteDirectory: "${remote_dir_path}",
       execCommand: "run commands after copy?"
      )
     ])
   ]
        )
      }
    }

  }
}
