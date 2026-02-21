pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "Building Docker Image"
                sh 'docker build -t website-app .'
            }
        }

        stage('Test') {
            steps {
                echo "Testing Application"
                sh 'echo Running Tests...'
            }
        }

        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                echo "Deploying to Production"
                sh '''
                docker stop website-container || true
                docker rm website-container || true
                docker run -d -p 80:80 --name website-container website-app
                '''
            }
        }
    }
}
