pipeline {
    agent any

    stages {

        stage('Clean Workspace') {
            steps {
                script {
                    deleteDir()
                }
            }
        }

        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'b066c20d-d98b-45e6-94fb-3c0b17ab9616', url: 'https://github.com/MELARBOUDI/SRE_Jenkins_test_3.git']]])
             }
        }

        stage('Version ansible') {
            steps {
                // Exécuter le playbook Ansible pour installer Nginx
                sh 'ansible --version'
            }
        }

        stage('Test Ping') {
            steps {
                // Exécuter le playbook Ansible pour installer Nginx
                sh 'ansible -i inventory.ini nginx_install.yml webserver -m ping '
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
