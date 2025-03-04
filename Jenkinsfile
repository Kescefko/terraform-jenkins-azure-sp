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
                sh 'terraform -version'
            }
        }

        stage('TF Init') {
            steps {
                sh 'terraform init'
            }
        }

        // stage('Terraform init') {
        //     steps {
        //         withCredentials([azureServicePrincipal(credentialsId: '0123456789', subscriptionIdVariable: 'SUBS_ID', clientIdVariable: 'CLIENT_ID', tenantIdVariable: 'TENANT_ID')]) {
        //             // tf init
        //             powershell 'terraform init'

        //             // Debugging certificate path - use semicolon (;) instead of &&
        //             powershell """
        //                 echo 'Checking certificate path...';
        //                 dir C:\\certificates\\tmpx3gp_atc.pem
        //             """

        //             // tf plan
        //             // powershell "terraform plan -var 'subscription_id=$SUBS_ID' -var 'tenant_id=$TENANT_ID' -var 'client_id=$CLIENT_ID' -var 'client_certificate_path=C:\\certificates\\tmpx3gp_atc.pem'"
        //             // Directly calling Git Bash using sh.exe
        //             bat "\"C:\\Program Files\\Git\\bin\\sh.exe\" -c \"terraform init && terraform plan -var \\\"subscription_id=${SUBS_ID}\\\" -var \\\"tenant_id=${TENANT_ID}\\\" -var \\\"client_id=${CLIENT_ID}\\\" -var \\\"client_certificate_path=C:/certificates/tmpx3gp_atc.pem\\\"\""
        //         }
        //     }
        // }
    }
}
