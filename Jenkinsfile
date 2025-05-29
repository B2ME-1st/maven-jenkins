pipeline {
  agent any

  tools {
    maven 'Maven'
  }

  environment {
    IMAGE_NAME = 'hello-world-app'
    IMAGE_TAG = 'latest'
  }

  stages {
    stage('Clone Repo') {
      steps {
        git branch: 'main', url: 'https://github.com/B2ME-1st/maven-jenkins.git'
      }
    }

    stage('Build with Maven') {
      steps {
        echo 'Building...'
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Build Docker Image') {
      steps {
        echo 'Containerizing...'
        sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
        // sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG -f path/to/Dockerfile .'
      }
    }

    stage('Run Docker Container') {
      steps {
        echo 'Running the container...'
        sh 'docker stop $IMAGE_NAME || true'
        sh 'docker rm $IMAGE_NAME || true'
        sh 'docker run -d -p 6060:6060 --name $IMAGE_NAME $IMAGE_NAME:$IMAGE_TAG'
      }
    }
  }
  post {
  success {
    echo "🎉 Build and deployment completed successfully!"
  }
  failure {
    echo "💥 Build failed! Check the logs for errors."
    }
  }
}

