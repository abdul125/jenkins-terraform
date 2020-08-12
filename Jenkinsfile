pipeline {
  agent {
    docker {
      image "bryandollery/terraform-packer-aws-alpine"
      args "-u root --entrypoint=''"
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
      stage("workspace") {
          steps {
              sh """
terraform workspace list
echo "*******************************************************************************************"
#--rm related to this ? java.io.IOException: Failed to rm container 'fb8fe24d0573864f51a141609c234bab3c1ea66b8c201b36eb42aa5bdfe8fbc3'.
docker ps -a 

terraform workspace select jenkins-lab-2
if [[ \$? -ne 0 ]]; then
  terraform workspace new jenkins-lab-2
fi
"""
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