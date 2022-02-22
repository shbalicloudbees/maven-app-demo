pipeline {
  agent {
    label "ubuntuos"
  }
  environment {
    VERSION = "$BUILD_TIMESTAMP"
    AWS_DEFAULT_REGION = "us-east-1"
    AWS_CREDS = credentials('shbaliaws')
  }
  stages {

    stage('Build project') {
      steps {
        sh "mvn clean install"
      }
    }

    stage('Check role ') {
      steps {

        echo "Whoami"
        sh "aws sts get-caller-identity" // or whatever

        echo "create tag"
        sh '''
              echo "Build tag: $BUILD_TAG"
        '''
      }

    }



  }

  post {
    always {
      println "run script to s3 bucket" // parse and send email
    }
  }

}
