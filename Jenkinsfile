pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'BCD50'  
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Aditi-24-05/DevOps_Assignment.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('BCD50') {
             sh './mvnw clean verify sonar:sonar -Dsonar.login=sqa_219f7117674fcc5aec62bf676ba5c5397f056c06'
            }
        }
    }
}
}
