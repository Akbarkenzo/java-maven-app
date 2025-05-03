pipeline {
    agent any

    tools {
        maven 'maven-3.9'
    }

    stages {
        stage('Build jar') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo "Building the Docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credential', passwordVariable: 'utmbarken', usernameVariable: 'barkenutm')]) {
                        sh 'docker build -t barkenutm/demo-app:jma-2.0 .'
                        sh "echo \$utmbarken | docker login -u \$barkenutm --password-stdin"
                        sh 'docker push barkenutm/demo-app:jma-2.0'
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
