pipeline {
    agent { label 'workers' }
    stages {      
        stage("Testing Ansible") {
            steps {
                withCredentials([string(credentialsId: 'golden_ssh_key.pub', variable: 'GOLD_KEY')]) {
                    script {
                        def extraVarsString = 'gold_key=$"{GOLD_KEY}"'
                        ansiblePlaybook(
                            disableHostKeyChecking: true,
                            installation: 'Ansible',
                            inventory: 'hosts.ini',
                            playbook: 'deploying_golden_key.yml',
                            credentialsId: 'ansible-jenkins',
                            extras: "--extra-vars '${extraVarsString}'"
                        )
                    }
                }
            
            }
        }            
    }      
}
