pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rachanack-rachhu/jenkins-imp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh '''
                    docker build -t flask-jenkins-app .
                    '''
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop any previous container (if running)
                    sh '''
                    docker rm -f flask-jenkins-container || true
                    docker run -d -p 5000:5000 --name flask-jenkins-container flask-jenkins-app
                    sleep 5
                    curl -f http://localhost:5000 || (echo "Container failed to start" && exit 1)
                    '''
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed."
        }
    }
}
