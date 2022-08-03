pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/Dev']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ponnamnagesh/TerraformEC2']]])            

          }
        }    
        stage ("Terraform Init") {
            steps {
                sh ('terraform init') 
            }
        }
        stage ("Terraform Plan") {
            steps {
                sh ('terraform plan') 
            }
        }
        stage ("Terraform Validate") {
            steps {
                sh ('terraform validate -json') 
            }
        }
        stage ("Terraform Action") {
            steps {
                echo "Terraform action is --> ${action}"
                sh ('terraform ${action} --auto-approve') 
                //sh ('terraform apply --auto-approve') 
                //sh ('terraform destroy --auto-approve')
           }
        }
    }
}

