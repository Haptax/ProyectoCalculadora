pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Restore') {
            steps {
                bat 'dotnet restore projectCalculadora.sln'
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build projectCalculadora.sln --configuration Release --no-restore'
            }
        }
        stage('Test') {
            steps {
                bat 'dotnet test calculadoraApp.Test/calculadoraApp.Test.csproj --configuration Release --no-build --no-restore'
            }
        }
        stage('Publish') {
            steps {
                bat 'dotnet publish calculadoraApp/calculadoraApp.csproj --configuration Release --no-build --output %WORKSPACE%\\publish'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'publish/**', fingerprint: true
        }
        failure {
            echo '❌ El pipeline falló en alguna etapa'
        }
    }
}