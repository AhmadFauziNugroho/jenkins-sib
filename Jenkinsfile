pipeline {
    agent any

    tools {
        maven 'maven-3.9'
    }
    
    stages {
        stage('Build jar') {
            steps {
                    sh 'maven package' 
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo "Building the Docker Image..."
                    withCredentials({usernamePassword(credential: 'docker-hub-repo', passwordVariable: 'USER')}) {
                        sh 'docker build -t sienaf/demo-app:jma-2.0
                        sh "echo \$PASS | docker login -u \$USER --password-stdin"
                        sh 'docker push sienaf/demo-app:jma-2.0'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}
