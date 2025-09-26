pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rachanack-rachhu/jenkins-imp.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run App') {
            steps {
                sh '''
                . venv/bin/activate
                nohup python3 app.py > flask.log 2>&1 &
                sleep 5
                curl -f http://localhost:5000 || (echo "App failed to start" && exit 1)
                '''
            }
        }
    }
}


