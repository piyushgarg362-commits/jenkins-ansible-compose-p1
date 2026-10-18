pipeline {
    agent any
    
    stages { 
        stage('Deploy using SSH Key') {
            steps {
                // Use the sshagent step to load and use the SSH private key
                sshagent(credentials: ['ansible-1']) {
                    // Run SSH commands securely here
                    sh '''
                    scp -r ssl ansible@172.31.15.113:/home/ansible/deployment/
                    scp docker-compose.yml docker-compose-2.yml nginx.conf .env .dockerignore devops@192.168.70.43:/home/devops/deployment/
                    ssh ansible@172.31.15.113 "sh -c 'if [ ! -d "/home/ansible/deployment/mysql_db" ]; then mkdir -p "/home/devops/deployment/mysql_db"; fi'"
                    ssh ansible@172.31.15.113 "cd /home/ansible/deployment/ && docker-compose -f docker-compose-2.yml down && docker-compose -f docker-compose-2.yml up -d"
                    '''
                }
            }
        }
    }
}
