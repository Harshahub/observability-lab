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

        stage('Deploy with Ansible') {
            steps {
                withCredentials([
                    sshUserPrivateKey(
                        credentialsId: 'ubuntu2-ssh',
                        keyFileVariable: 'SSH_KEY',
                        usernameVariable: 'SSH_USER'
                    )
                ]) {
                    sh '''
                        chmod 600 "$SSH_KEY"

                        ansible-playbook \
                          -i ansible/inventory \
                          ansible/deploy.yaml \
                          --private-key "$SSH_KEY" \
                          -u "$SSH_USER"
                    '''
                }
            }
        }
    }
}
