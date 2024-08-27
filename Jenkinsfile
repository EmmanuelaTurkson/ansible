pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main', url: 'https://github.com/EmmanuelaTurkson/ansible.git'
            }
        }

        stage('Build') {
            steps {
                ansible-playbook -i hosts.yml config_routers.yml
            }
        }
        

        stage('Deploy') {
            steps {
                ansible-playbook -i hosts.yml routing_config.yml
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/backups/*.txt', allowEmptyArchive: true
            cleanWs()
        }
    }
}
