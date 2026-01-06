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
                sh 'dotnet restore projectCalculadora.sln'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build projectCalculadora.sln --configuration Release --no-restore'
            }
        }
        stage('Test') {
            steps {
                sh 'dotnet test calculadoraApp.Test/calculadoraApp.Test.csproj --configuration Release --no-build --no-restore'
            }
        }
        stage('Publish') {
            steps {
                sh 'dotnet publish calculadoraApp/calculadoraApp.csproj --configuration Release --no-build --output ${WORKSPACE}/publish'
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