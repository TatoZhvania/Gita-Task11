pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // This ensures Jenkins polls for changes every minute
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'stage', url: 'https://github.com/TatoZhvania/Gita-Task11.git'
            }
        }
        stage('User Input') {
            steps {
                script {
                    def userInput = input message: 'Do you want to proceed?', parameters: [choice(name: 'Proceed', choices: ['yes', 'no'], description: 'Select Yes to proceed')]
                    if (userInput == 'yes') {
                        echo "User chose YES, proceeding to next stage..."
                    } else {
                        error("User chose NO, stopping the pipeline.")
                    }
                }
            }
        }
        stage('Parallel Execution') {
            parallel {
                stage('Success Curl') {
                    steps {
                        sh 'curl google.ge'
                    }
                }
                stage('Failing Curl') {
                    steps {
                        script {
                            def result = sh(script: 'curl error.ueczo.com', returnStatus: true)
                            if (result != 0) {
                                echo "this url does not work"
                            }
                        }
                    }
                }
            }
        }
    }
    post {
        always {
            echo "Pipeline execution completed successfully."
        }
    }
}
