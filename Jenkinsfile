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
                sh 'echo "Skipping tests..."'
            }
        }
         stage('Build Docker Image') {
            steps {
                sh 'echo "Skipping tests..."'
            }
        }
         stage('Run Tests') {
    steps {
       sh 'echo "Skipping tests..."'
    }
}

     stage('Deploy with Docker Compose') {
            steps {
                sh 'echo "Skipping tests..."'
            }
        }
stage('Push to Docker Hub') {
    steps {
        sh 'echo "Skipping tests..."'
        }
    }

}
}
