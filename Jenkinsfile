pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'dejanristevski96@gmail.com'
    }

    stages {
        stage('Freestyle Job Simulation') {
            steps {
                script {
                    echo 'Executing shell script for system status report...'
                    sh '''
                    echo "System Status Report"
                    uname -a
                    df -h
                    '''
                }
            }
        }

        stage('Automate GitHub Repository Pull') {
            steps {
                git url: 'https://github.com/therdean/iwec-jenk.git', branch: 'main', credentialsId: 'github-pat'
            }
        }

        stage('Declarative Pipeline Tasks') {
            steps {
                echo 'Exploring Declarative Pipeline concepts...'
                sh '''
                echo "Checkout phase completed."
                echo "Build phase simulated."
                '''
            }
        }

        stage('Send Notifications') {
            steps {
                emailext(
                    subject: "Pipeline Build Notification - ${currentBuild.fullDisplayName}",
                    body: "Pipeline build status: ${currentBuild.currentResult}",
                    to: "${env.EMAIL_RECIPIENT}"
                )
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            emailext(
                subject: "Pipeline Failed - ${currentBuild.fullDisplayName}",
                body: "Pipeline build failed with status: ${currentBuild.currentResult}",
                to: "${env.EMAIL_RECIPIENT}"
            )
        }
    }
}
