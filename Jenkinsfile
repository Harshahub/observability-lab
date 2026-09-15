pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Repository') {
            steps {
                sh 'echo "Repository checkout successful"'
                sh 'ls -R'
            }
        }

        stage('Validate Ansible') {
            steps {
                sh 'ansible-playbook --syntax-check ansible/deploy.yaml'
            }
        }
    }
}
