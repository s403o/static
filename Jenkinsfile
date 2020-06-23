pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      parallel {
        stage('Lint HTML') {
          steps {
            sh 'sudo apt-get install -y tidy'
          }
        }

        stage('error') {
          steps {
            sh 'tidy -q -e *.html'
          }
        }

      }
    }

    stage('Upload to AWS') {
      steps {
        withAWS(region: 'us-east-2', credentials: 'aws-static') {
          sh 'echo "Hello World with AWS"'
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'jenkins0')
        }

      }
    }

  }
}