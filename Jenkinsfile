@Library('roche-library') _
pipeline {
  agent {
    label "ubuntuos"
  }
  environment {
    VERSION = "$BUILD_TIMESTAMP"
    AWS_DEFAULT_REGION = "us-east-1"
    ID_GIT_COMMIT = "${GIT_COMMIT}"
    TIMESTAMP_ROCHE= getTimeStamp()
    ROCHE_TAG="${GIT_COMMIT}-${BUILD_TAG}-${TIMESTAMP_ROCHE}"
 //   AWS_CREDS = credentials('shbaliaws')
  }
  stages {
/**
    stage('Build project') {
      steps {
       sh "mvn clean package"
      }
    }*/

    stage('Check role ') {
      steps {
/*
        echo "Whoami"
        sh '''
          export AWS_PROFILE=cloudbees-ps
          /tmp/opscore iam refresh --account cloudbees-ps --role infra-admin --profile cloudbees-ps
          aws sts get-caller-identity
          mkdir outputfolder 
          cp -a target/. outputfolder
        ''' 
*/
        echo "create tag"
        sh '''
            
          
             echo " build tag $ROCHE_TAG"
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
