pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Cloner le dépôt Git contenant la configuration Ansible et les fichiers nécessaires
                git 'https://github.com/MELARBOUDI/SRE_Jenkins_test_3.git'
            }
        }

        stage('Install Ansible') {
            steps {
                // Installer Ansible sur l'agent Jenkins (Ubuntu)
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y ansible'
            }
        }

        stage('Deploy Nginx') {
            steps {
                // Exécuter le playbook Ansible pour installer Nginx
                sh 'ansible-playbook -i inventory.ini nginx_install.yml'
            }
        }
    }

    post {
        success {
            echo 'Nginx a été installé avec succès sur le serveur distant Ubuntu.'
        }
        failure {
            echo 'L\'installation de Nginx a échoué.'
        }
    }
}
