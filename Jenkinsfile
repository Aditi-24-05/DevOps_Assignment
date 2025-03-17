pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'BCD50'  
        IMAGE_NAME = "devops_assignment-petclinic"
        CONTAINER_NAME = "devops_assignment-petclinic-1"
        DB_IMAGE = "mysql:9.1"
        DB_CONTAINER = "devops_assignment-mysql-1"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Aditi-24-05/DevOps_Assignment.git'
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package -X'
            }
        }
         stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
         stage('Run Tests') {
    steps {
        sh './mvnw test'
    }
}

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('BCD50') {
             sh './mvnw clean verify sonar:sonar -Dsonar.login=sqa_917d05cf65ce2af1b023fd87c6db60dd0006aaff'
            }
        }
    }
     stage('Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose down'
                    sh 'docker-compose up -d'
                }
            }
        }
stage('Push to Docker Hub') {
    steps {
        script {
            withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials-id', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                sh 'docker tag $IMAGE_NAME $DOCKER_USER/$IMAGE_NAME:latest'
                sh 'docker push $DOCKER_USER/$IMAGE_NAME:latest'
            }
        }
    }
}
}
}
