pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('SSH Test') {
            steps {
                sshagent(['ec2-deploy-key']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ec2-user@172.31.13.64 "hostname"
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['ec2-deploy-key']) {
                    sh '''
                        scp -o StrictHostKeyChecking=no index.html style.css ec2-user@172.31.13.64:/usr/share/nginx/html/
                    '''
                }
            }
        }

    }
}