pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }
    stage('Upload to AWS.') {
      steps {
        withCredentials([[
          $class: 'AmazonWebServicesCredentialsBinding', 
          credentialsId: 'my-aws-credentials',
          ACCESS_KEY: 'ASIA47YS73AF75NICPER',
          SECRET_KEY: '=2NdD7GyC0YPokj6xMCV0L3asZMwJwZG+FpsGVakz',
          SESSION_TOKEN: 'FwoGZXIvYXdzEBAaDMMUkMEixlzNW0DvTSLHAZtD8R9nLI3lI9m4PZWGmq+YY2pVRMEjXxvNW9nXHo6PQEv/jUik8lCRnHDCjbg+/YkMv3S45XIoEUCy1d+KgUfyIt1fGw5QXW9/KJaRewGwXB+B3sZ4a4m0R3v5eVVHp8ryefYTNepogB7xR3BZLx/saWumD5jDtZrTuqswLz3hOVouD10vG+Vjqrb+tv7dbdTZ5DL/6LmAWGvOWicbNb0U0EQZIpRxJUKF5GB6vcLyA6nry+YH89msNuRGjckuIWQ+zxzfpvEoqYWj9gUyLdrDeuYoauNrn9hRgqQ1wEah0xHRX9xymExNrMTIIled1onetWZy2R/3N2+W7w==']]) { }
        withAWS(region:'us-east-1',credentials:'my-aws-credentials') {
        sh 'echo "Uploading content with AWS creds"'
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-jenkins-bucket')
        }
      }
    }
  }
}
