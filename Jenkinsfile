pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage('Deploy to QA') {
            steps {
                echo "Deploying to QA"
            }
        }

        stage('Pull Docker Images') {
            parallel {
                stage('Pull GoRest Image') {
                    steps {
                        bat 'docker pull kalairam82/gorestapi:1.0'
                    }
                }
                
                stage('Pull Booking Image') {
                    steps {
                        bat 'docker pull kalairam82/bookingapi:1.0'
                    }
                }
            }
        }

        stage('Prepare Newman Results Directory') {
            steps {
                bat 'mkdir "newman"'
            }
        }

        stage('Run API Test Cases in Parallel') {
            parallel {
                stage('Run GoRest Tests') {
                    steps {
                        bat 'docker run --rm -v %cd%\\newman:/app/results kalairam82/gorestapi:1.0'
                    }
                }
                
                stage('Run Booking Tests') {
                    steps {
                        bat 'docker run --rm -v %cd%\\newman:/app/results kalairam82/bookingapi:1.0'
                    }
                }
            }
        }

           stage('Publish HTML Extra Reports') {
            parallel {
                stage('Publish GoRest Report') {
                    steps { 
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'newman',
                reportFiles: 'gorest.html',
                reportName: 'gorest HTML Report'
            ])
        }
    }

            
                stage('Publish booking Report') {
                    steps {    
                   publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'newman',
                reportFiles: 'booking.html',
                reportName: 'booking HTML Report'
            ])
        }
     }
  }
}

        stage('Deploy to PROD') {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}