pipeline {
    agent { label "ubuntuos" }

    stages {
        stage ('Build project') {
            steps {
                sh "mvn clean install"
            }
        }
        
        stage('assume role ') {
            steps {
                withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'shbaliaws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                     sh "aws sts get-caller-identity" // or whatever
                }
          
            }
        }
    }
    
    
    post {
        always {
            echo 'archive to S3'
        }
        
    }
}
