pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Srinivasgonu/Jenkins-Assign.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment step placeholder'
            }
        }
    }
}
