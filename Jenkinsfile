pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-python-flask-app'
        DOCKER_HUB_USERNAME = credentials('regalflit0042')
        DOCKER_HUB_PASSWORD = credentials('Regalflit@0042')
    }

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                    sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                    sh "docker tag $IMAGE_NAME $DOCKER_HUB_USERNAME/$IMAGE_NAME"
                    sh "docker push $DOCKER_HUB_USERNAME/$IMAGE_NAME"
                }
            }
        }
    }
}

