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
                sh 'docker run -d -p 367:80 --name portfolio portfolio-site'
            }
        }
    }
}