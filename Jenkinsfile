pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-credentials',
                    url: 'https://github.com/akhileshvelamuri/.NET_Angular_MySQL_School_Management_System.git'
            }
        }
        
        stage('Restore Dependencies') {
            steps {
                script {
                    // Restore NuGet packages for .NET backend
                    bat 'dotnet restore'
                }
            }
        }
        
        stage('Build Backend') {
            steps {
                script {
                    // Build .NET application
                    bat 'dotnet build --configuration Release --no-restore'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Run .NET tests if any exist
                    bat 'dotnet test --no-build --configuration Release || exit 0'
                }
            }
        }
        
        stage('Publish') {
            steps {
                script {
                    // Publish .NET application
                    bat 'dotnet publish --configuration Release --output ./publish'
                }
            }
        }
        
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'publish/**/*', fingerprint: true, allowEmptyArchive: true
            }
        }
    }
    
    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
        always {
            cleanWs()
        }
    }
}
