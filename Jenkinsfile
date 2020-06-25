pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      parallel {
        stage('Lint HTML') {
          steps {
            sh 'tidy -q -e *.html'
          }
        }

        stage('Build') {
          steps {
            sh 'echo "Hello World"'
            sh '''sh \'\'\'
                     echo "Multiline shell steps works too"
                     ls -lah
                 \'\'\''''
          }
        }

      }
    }

    stage('Upload to AWS') {
      steps {
        withAWS(region: 'us-west-2', credentials: 'Jenkins') {
          sh 'echo "Uploading content with AWS creds"'
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'jenkins-bucket-alex')
        }

      }
    }

  }
}