pipeline {
    agent any
    environment {
        SSHKEY = credentials('jenkins-ansible')
        ANSIBLE_HOST_KEY_CHECKING = 'False'
        ANSIBLE_SCP_IF_SSH = 'True'
    }
    stages {
        stage ("Build") {
            steps {
                sh 'docker build -t myimage:$BUILD_NUMBER .'
            }
        }
        stage(" Test") {
           steps {
                ansiblePlaybook credentialsId: 'jenkins-ansible', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'inventory.ini', playbook: 'docker_playbook.yaml'
            }    
        }    
    }
}
