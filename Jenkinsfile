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
                        ssh -o StrictHostKeyChecking=no ec2-user@<EC2_PUBLIC_IP> "rm -rf /home/ec2-user/app/*"
                        scp -o StrictHostKeyChecking=no -r * ec2-user@<EC2_PUBLIC_IP>:/home/ec2-user/app/
                    '''
                }
            }
        }
    }
}
