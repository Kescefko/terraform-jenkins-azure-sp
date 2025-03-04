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
                withCredentials([azureServicePrincipal(credentialsId: '0123456789', subscriptionIdVariable: 'SUBS_ID', clientIdVariable: 'CLIENT_ID', tenantIdVariable: 'TENANT_ID'), file(credentialsId: '915fdc5c-1e4b-43d5-95c4-cf1a4bb60980', variable: 'CLIENT_CERT_PATH')]) {
                    sh 'terraform init'
                    sh "terraform plan -var 'subscription_id=$SUBS_ID' -var 'tenant_id=$TENANT_ID' -var 'client_id=$CLIENT_ID' -var 'client_certificate_path=$CLIENT_SECRET'"
                    sh "terraform destroy --auto-approve -var 'subscription_id=$SUBS_ID' -var 'tenant_id=$TENANT_ID' -var 'client_id=$CLIENT_ID' -var 'client_secret=$CLIENT_SECRET'"
                }
            }
        }
    }
}
