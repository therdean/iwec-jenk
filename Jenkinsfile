pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'dejanristevski96@gmail.com'
    }

    stages {
        stage('Freestyle Job Simulation') {
            steps {
                script {
                    echo 'Executing system status report on Windows...'
                    bat '''
                    echo System Status Report
                    systeminfo
                    wmic logicaldisk get size,freespace,caption
                    '''                }
            }
        }

        stage('Automate GitHub Repository Pull') {
            steps {
                git url: 'https://github.com/therdean/iwec-jenk.git', branch: 'main', credentialsId: 'github-pat'
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
