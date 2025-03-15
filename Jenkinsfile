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
                sh './mvnw clean package'
            }
        }
         stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
          stage('Run Tests in Container') {
            steps {
                sh 'docker run --rm $IMAGE_NAME mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('BCD50') {
             sh './mvnw clean verify sonar:sonar -Dsonar.login=sqa_219f7117674fcc5aec62bf676ba5c5397f056c06'
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
}
}
