pipeline {
    agent any
    environment {
        SSHKEY = credentials('jenkins-ansible')
        ANSIBLE_HOST_KEY_CHECKING = 'False'
        ANSIBLE_SCP_IF_SSH = 'True'
    }
    stages {
        stage ("SCM checkout") {
            steps {
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/E01382/training'
                
            }
        }
        stage ("Build") {
            steps {
                sh 'docker build -t myimage:$BUILD_NUMBER .'
            }
        }
        stage(" Test") {
           steps {
                ansiblePlaybook credentialsId: 'jenkins-ansible', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'inventory.ini', playbook: 'nginx.yaml'
            }    
        }    
    }
}
