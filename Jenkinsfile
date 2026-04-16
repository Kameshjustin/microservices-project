pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git(
                    branch: 'main',
                    credentialsId: 'git-cred-akjus',
                    url: 'https://github.com/Kameshjustin/microservices-project.git'
                )
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['micro-cred']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no ubuntu@13.53.83.53 \
                           "set -e && \
                            cd /home/ubuntu/microservices-project &&
                            rm -rf microservices-project || true &&
                            git clone https://github.com/Kameshjustin/microservices-project.git /home/ubuntu/microservices-project && \
                            cd /home/ubuntu/microservices-project && \
                            chmod +x clone.sh && \
                            ./clone.sh && \
                            docker-compose down || true && \
                            docker system prune -f && \
                            docker-compose up -d --build"
                    '''
                }
            }
        }

    }
}
