pipeline {
  agent any

  tools {
    maven 'Maven'
  }

  environment {
    IMAGE_NAME = 'hello-world-app'
  }

  stages {
    stage('Clone Repo') {
      steps {
        git 'https://github.com/B2ME-1st/maven-jenkins.git'
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
        sh 'docker build -t $IMAGE_NAME .'
      }
    }

    stage('Run Docker Container') {
      steps {
        echo 'Running the container...'
        sh 'docker stop $IMAGE_NAME || true'
        sh 'docker rm $IMAGE_NAME || true'
        sh 'docker run -d -p 6060:6060 --name $IMAGE_NAME $IMAGE_NAME'
      }
    }
  }
}
