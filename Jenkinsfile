pipeline {
  agent {
    docker {
      image "bryandollery/terraform-packer-aws-alpine"
      args "-u root --entrypoint='' --rm"
    }
  }
  environment {
    CREDS = credentials('abdul-aws-creds')
    AWS_ACCESS_KEY_ID = "${CREDS_USR}"
    AWS_SECRET_ACCESS_KEY = "${CREDS_PSW}"
    OWNER = "abdul"
    PROJECT_NAME = 'web-server'
    AWS_PROFILE="kh-labs"
    TF_NAMESPACE="abdul"
  }
  
  stages {
      stage("init") {
          steps {
              sh 'make init'
          }
      }

      stage("plan") {
          steps {
              sh 'make plan'
          }
      }
    
      stage("apply") {
          steps {
              sh 'make apply'
          }
      }
    
  }
}
