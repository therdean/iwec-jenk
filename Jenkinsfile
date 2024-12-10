pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'your-email@example.com'
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
                git url: 'https://github.com/your-username/your-repo.git', branch: 'main', credentialsId: 'github-pat'
                sh 'ls -l'
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

        stage('Parallel File Copy') {
            parallel {
                stage('Copy to Location A') {
                    steps {
                        script {
                            if (currentBuild.currentResult == 'SUCCESS') {
                                sh 'echo "Copying files to Location A..."'
                            }
                        }
                    }
                }
                stage('Copy to Location B') {
                    steps {
                        script {
                            if (currentBuild.currentResult == 'SUCCESS') {
                                sh 'echo "Copying files to Location B..."'
                            }
                        }
                    }
                }
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
