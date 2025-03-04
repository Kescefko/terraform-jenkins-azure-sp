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
                bat 'terraform -version'
            }
        }
    }
}
