pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                // Checkout code from GitHub and specify the branch
                git branch: 'main', url: 'https://github.com/xchshark/JenkinsSeleniumWebDriver_04_08_24'
            }
        }

        stage('Set up .NET Core') {
            steps {
                bat '''
                echo Installing .NET SDK 6.0
                choco install dotnet-sdk -y --version=6.0.100
                '''
            }
        }

        // Премахнати стъпки за деинсталиране на Chrome
        // Премахнати стъпки за изтегляне и инсталиране на ChromeDriver

        stage('Restore dependencies') {
            steps {
                // Restore dependencies using the solution file
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }
        }

        stage('Build') {
            steps {
                // Build the project using the solution file
                bat 'dotnet build SeleniumBasicExercise.sln --no-restore'
            }
        }

        stage('Run TestProject1 tests') {
            steps {
                bat '''
                echo "Running TestProject1 tests"
                dotnet test TestProject1/TestProject1.csproj --verbosity normal
                '''
            }
        }

        stage('Run TestProject2 tests') {
            steps {
                bat '''
                echo "Running TestProject2 tests"
                dotnet test TestProject2/TestProject2.csproj --verbosity normal
                '''
            }
        }

        stage('Run TestProject3 tests') {
            steps {
                bat '''
                echo "Running TestProject3 tests"
                dotnet test TestProject3/TestProject3.csproj --verbosity normal
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            junit '**/TestResults/*.trx'
        }
    }
}
