pipeline {
    agent any

    environment {
        ANSIBLE_HOST = "ubuntu@54.165.114.174" // Ansible server public IP
        PEM_KEY_PATH = "/var/lib/jenkins/.ssh/kuberneteskey.pem"
        PLAYBOOK_PATH = "/home/ubuntu/deploy-docker-container.yml"
        INVENTORY_PATH = "/etc/ansible/hosts"
    }

    stages {
        stage('Trigger Ansible Playbook') {
            steps {
                script {
                    sh """
                    ssh -o StrictHostKeyChecking=no -i $PEM_KEY_PATH $ANSIBLE_HOST \\
                    ansible-playbook $PLAYBOOK_PATH -i $INVENTORY_PATH
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Playbook executed successfully!'
        }
        failure {
            echo '❌ Playbook execution failed!'
        }
    }
}

