pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-creds', url: 'https://github.com/HuuBanghoopa/jenkins.git'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    def dotnetHome = tool name: 'dotnet-core', type: 'com.cloudbees.jenkins.plugins.customtools.CustomTool'
                    env.PATH = "${dotnetHome}\\bin;${env.PATH}"
                }
                powershell 'dotnet restore'
                powershell 'dotnet build --configuration Release'
            }
        }
        
        stage('Test') {
            steps {
                powershell 'dotnet test'
            }
        }
        
        stage('Publish') {
            steps {
                powershell 'dotnet publish -c Release -o published'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}

