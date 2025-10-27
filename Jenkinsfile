pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo '🔹 Cloning repository from GitHub...'
                git branch: 'main', url: 'https://github.com/moaaz-abdelkarim/my_app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo '🔹 Building Docker image...'
                    sh 'docker build -t nodejs-app:${BUILD_NUMBER} .'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo '🔹 Running Docker container on port 3000...'
                    sh '''
                    docker rm -f nodejs-container || true
                    docker run -d -p 3000:3000 --name nodejs-container nodejs-app:latest
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
            sh 'docker ps'
        }
        failure {
            echo '❌ Pipeline failed. Check logs.'
        }
    }
}
