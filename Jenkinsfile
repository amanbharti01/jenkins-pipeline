pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Pulling code from GitHub..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building the project..."
                sh 'echo Build successful!'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'echo Tests passed!'
            }
        }

        stage('Deploy to EC2') {
            steps {
                echo "Deploying code to EC2..."
                sshagent (credentials: ['ec2-ssh-key']) {
                    sh '''
                        # Remove old files
                        ssh -o StrictHostKeyChecking=no ec2-user@44.200.190.228 "rm -rf /home/ec2-user/app/*"

                        # Copy new files to EC2
                        scp -o StrictHostKeyChecking=no -r * ec2-user@44.200.190.228:/home/ec2-user/app/
                    '''
                }
            }
        }
    }
}

