pipeline {
    agent any
    environment {
  PATH = "${PATH}:${getTerraformpath()}"
}
stages {
  stage('s3 - create bucket'){
  steps{
  sh "ansible-playbook s3-bucket.yml"
      }
    }
  stage('TerraformINIT and apply - dev') {
    steps{
      sh returnStatus: true, script: 'terraform workspace new dev'
      sh "terraform init"
      sh "ansible-playbook terraform.yml"
    }
  }
  stage('TerraformINIT and apply - prod') {
    steps{
      sh returnStatus: true, script: 'terraform workspace new prod'
      sh "terraform init"
      sh "ansible-playbook terraform.yml -e app_env=prod"
    }
  }
}
}

def getTerraformpath(){
def tfHome = tool name: 'Terraform-0.12', type: 'terraform'
return tfHome
}
