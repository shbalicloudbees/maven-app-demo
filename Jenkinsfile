pipeline {
  agent {
    label "ubuntuos"
  }
  environment {
    VERSION = "$BUILD_TIMESTAMP"
    AWS_DEFAULT_REGION = "us-east-1"
 //   AWS_CREDS = credentials('shbaliaws')
  }
  stages {

    stage('Build project') {
      steps {
        sh "mvn clean package"
      }
    }

    stage('Check role ') {
      steps {

        echo "Whoami"
        sh '''
          export AWS_PROFILE=cloudbees-ps
          /tmp/opscore iam refresh --account cloudbees-ps --role infra-admin --profile cloudbees-ps
          aws sts get-caller-identity
        ''' 

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
