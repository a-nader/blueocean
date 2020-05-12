pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'echo "Hello World2223"'
        sh '''
                     echo "Multiline shell steps works too2223333"
                     ls -lah
                 '''
      }
    }

    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }

    stage('Security Scan') {
      steps {
        aquaMicroscanner(imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'aaaa')
      }
    }

    stage('Upload to AWS') {
      steps {
        withAWS(region: 'us-east-2', credentials: 'aws-static') {
          sh 'echo "Uploading content with AWS creds"'
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'static-jenkins-pipeline')
        }

      }
    }

  }
}