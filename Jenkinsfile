pipeline {
    agent any

    tools {
        maven 'maven-3.9.9'
    }

    stages {
        stage('Build Jar') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Build and Push Image') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: 'docker-hub-credential',
                        passwordVariable: 'PASS',
                        usernameVariable: 'USER'
                    )]) {
                        echo 'Building Docker image...'
                        sh 'docker build -t azeshion21/demo-app:jma-2.0 .'
                        
                        echo 'Logging into Docker Hub...'
                        sh "echo \$PASS | docker login -u \$USER --password-stdin"
                        
                        echo 'Pushing image to Docker Hub...'
                        sh 'docker push azeshion21/demo-app:jma-2.0'
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying the application...'
                    // Add deployment commands here
                }
            }
        }
    }
}
