pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Build image') {
            steps {
                sh 'docker build -t portfolio-site .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker rm -f portfolio || true'
                sh 'docker run -d --restart unless-stopped -p 367:80 --name portfolio portfolio-site'
            }
        }
        stage('Smoke test') {
            steps {
                sh 'sleep 3'
                sh 'curl -fsS -o /dev/null http://host.docker.internal:367'
            }
        }
    }
}