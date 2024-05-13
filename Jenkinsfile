pipeline {
    agent any

    environment {
        HOME = '.'
    }

    tools {
        // Ensure NodeJS is installed via Jenkins' tool configuration
        nodejs 'NodeJS'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Initialize EB Application') {
            steps {
                // Initialize Elastic Beanstalk application
                sh 'eb init -p node.js weatherapp --region us-east-1'
            }
        }
        stage('Deploy to AWS Elastic Beanstalk') {
            steps {
                // Package and deploy the application
                sh 'zip -r weatherapp.zip build'
                sh 'eb deploy -l $BUILD_ID'
            }
        }
    }
}
