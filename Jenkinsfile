pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }
    stage("Test") {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-static']]) {
          sh 'env'
          sh 'aws s3 ls'
        }
    }
    stage('Upload to AWS.') {
      steps {
        withAWS(region:'us-east-1',credentials:'aws-static') {
        sh 'echo "Uploading content with AWS creds"'
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-jenkins-bucket')
        }
      }
    }
  }
}
