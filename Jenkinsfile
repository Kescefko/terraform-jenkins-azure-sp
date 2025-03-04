pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the 'main' branch from the specified GitHub repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Kescefko/terraform-jenkins-azure-sp.git']])
            }
        }

        stage('TF Version') {
            steps {
                powershell 'terraform -version'
            }
        }

        stage('TF Init') {
            steps {
                powershell 'terraform init'
            }
        }

        stage('Terraform init') {
            steps {
                withCredentials([azureServicePrincipal(credentialsId: '0123456789', subscriptionIdVariable: 'SUBS_ID', clientIdVariable: 'CLIENT_ID', tenantIdVariable: 'TENANT_ID')]) {
                    // tf init
                    powershell 'terraform init'

                     // Debugging certificate path
                    powershell "echo 'Checking certificate path...' && dir C:\\certificates\\tmpx3gp_atc.pem"

                    // tf plan
                    powershell "terraform plan -var 'subscription_id=$SUBS_ID' -var 'tenant_id=$TENANT_ID' -var 'client_id=$CLIENT_ID' -var 'client_certificate_path=C:\\certificates\\tmpx3gp_atc.pem'"
                }
            }
        }
    }
}
