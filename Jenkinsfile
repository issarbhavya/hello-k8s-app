pipeline {
  agent any

  environment {
    IMAGE_NAME = "bissar/hello-k8s"
  }

  stages {
    stage('Build') {
      steps {
        echo "🔨 Building Docker image..."
        sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
      }
    }

    stage('Push') {
      steps {
        echo "🚀 Logging in and pushing to Docker Hub..."
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
          sh 'docker push $IMAGE_NAME:$BUILD_NUMBER'
        }
      }
    }

    stage('Done') {
      steps {
        echo "✅ Image pushed: $IMAGE_NAME:$BUILD_NUMBER"
      }
    }
  }
}

