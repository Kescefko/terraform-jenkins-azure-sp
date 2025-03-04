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
        //         withCredentials([azureServicePrincipal(credentialsId: 'CertAuthTestApp', subscriptionIdVariable: 'SUBS_ID', clientIdVariable: 'CLIENT_ID', tenantIdVariable: 'TENANT_ID'), certificate(credentialsId: '8bb5a193-07e2-4e42-ba14-b15cf3c0a8f0', keystoreVariable: 'CERT_PATH') ]) {
        //             // tf plan
        //             // sh "terraform plan -var 'subscription_id=$SUBS_ID' -var 'tenant_id=$TENANT_ID' -var 'client_id=$CLIENT_ID' -var 'client_certificate_path=XXXXX'"

        //             sh '''
        //                 echo "Using Azure Service Principal"
        //                 echo "Subscription ID: $SUBS_ID"
        //                 echo "Tenant ID: $TENANT_ID"
        //                 echo "Client ID: $CLIENT_ID"
                        
        //                 echo "Using certificate stored at: $CERT_PATH"

        //                 # Convert certificate if needed (e.g., extract private key and cert)
        //                 # openssl pkcs12 -in "$CERT_PATH" -nodes -out cert.pem -password pass:$CERT_PASS

        //                 # Terraform Plan with Certificate Path
        //                 terraform plan -var "subscription_id=$SUBS_ID" \
        //                     -var "tenant_id=$TENANT_ID" \
        //                     -var "client_id=$CLIENT_ID" \
        //                     -var "client_certificate_path=$CERT_PATH"
        //             '''
        //         }
        //     }
        // }


        stage('Terraform init') {
            steps {
                withCredentials([azureServicePrincipal(credentialsId: 'CertAuthTestApp', subscriptionIdVariable: 'SUBS_ID', clientIdVariable: 'CLIENT_ID', tenantIdVariable: 'TENANT_ID'), file(credentialsId: 'certfile', variable: 'CERT_PATH') ]) {
                    // tf plan
                    // sh "terraform plan -var 'subscription_id=$SUBS_ID' -var 'tenant_id=$TENANT_ID' -var 'client_id=$CLIENT_ID' -var 'client_certificate_path=XXXXX'"

                    sh '''
                        echo "Using Azure Service Principal"
                        echo "Subscription ID: $SUBS_ID"
                        echo "Tenant ID: $TENANT_ID"
                        echo "Client ID: $CLIENT_ID"
                        
                        echo "Using certificate stored at: $CERT_PATH"

                        # Convert certificate if needed (e.g., extract private key and cert)
                        # openssl pkcs12 -in "$CERT_PATH" -nodes -out cert.pem -password pass:$CERT_PASS

                        # Terraform Plan with Certificate Path
                        terraform plan -var "subscription_id=$SUBS_ID" \
                            -var "tenant_id=$TENANT_ID" \
                            -var "client_id=$CLIENT_ID" \
                            -var "client_certificate_path=$CERT_PATH"
                    '''
                }
            }
        }
    }
}
