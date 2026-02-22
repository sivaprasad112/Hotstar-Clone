pipeline {
    agent {
        node {
            label 'AGENT1'
        }
    }

    environment {
        APP_NAME = "hotstar"
        NODE_ENV = "production"
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install --production'
            }
        }

        stage('Run with PM2') {
            steps {
                sh '''
                pm2 describe hotstar > /dev/null 2>&1 && pm2 delete hotstar || true
                pm2 start npm --name hotstar -- start
                pm2 save
                pm2 status
                '''
            }
        }
    }
}
