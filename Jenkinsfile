pipeline {
    agent any
    
    tools {
        nodejs 'NodeJS'  // Assuming NodeJS is installed in Jenkins
        maven 'Maven'    // Assuming Maven is installed in Jenkins
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/<your-username>/<your-repo>.git'
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Run Backend') {
            steps {
                dir('backend') {
                    sh 'mvn spring-boot:run &'
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm start &'
                }
            }
        }
    }

    post {
        always {
            cleanWs()  // Clean workspace after the build
        }
    }
}

