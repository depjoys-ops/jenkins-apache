pipeline {
    agent any

    // Define the path to the Apache HTTP Server error log file
    environment {
        LOG_FILE = '/var/log/apache2/error.log'
    }

    stages {

        // Stage to install Apache HTTP Server
        stage('Install Apache') {
            steps {
                script {
                    // Update package lists and install Apache HTTP Server
                    sh 'sudo apt-get update'
                    sh 'sudo apt-get install -y apache2'
                    // Start the Apache service
                    sh 'sudo systemctl start apache2'
                }
            }
        }

        // Stage to check if Apache HTTP Server is started
        stage('Check Started Apache') {
            steps {
                script {
                    // Check the status of the Apache service and display the output
                    sh 'sudo systemctl status apache2 | cat'
                }
            }
        }

        // Stage to check Apache HTTP Server logs for errors
        stage('Check Apache Logs') {
            steps {
                script {
                    // Use grep to search for 4xx and 5xx errors in the Apache error log file
                    def errors = sh(script: "sudo grep -E ' 4[0-9]{2} | 5[0-9]{2} ' ${env.LOG_FILE} | wc -l", returnStdout: true).trim()
                    def errorCount = errors.toInteger()

                    // If errors are found, fail the pipeline with an error message
                    if (errorCount > 0) {
                        error "Found ${errorCount} 4xx or 5xx errors in Apache HTTP Server logs"
                    }
                }
            }
        }

        // Stage to stop Apache HTTP Server
        stage('Stop Apache') {
            steps {
                script {
                    // Stop the Apache service
                    sh 'sudo systemctl stop apache2'
                }
            }
        }
        
        // Stage to check if Apache HTTP Server is stopped
        stage('Check Stopped Apache') {
            steps {
                script {
                    // Check the status of the Apache service again to ensure it is stopped
                    sh 'sudo systemctl status apache2 | cat'
                }
            }
        }
    }
}
