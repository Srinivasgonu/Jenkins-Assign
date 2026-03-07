pipeline {
    agent { label 'slave-1' }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Security Scan') {
            steps {
                sh 'trivy fs --exit-code 1 --severity HIGH,CRITICAL .'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Deploy to The Application Server') {
            steps {
                sshagent(['ubuntu']) {
                    sh '''
                    scp -o StrictHostKeyChecking=no target/maven-simple-1.0-SNAPSHOT.jar ubuntu@98.80.138.134 :/home/ubuntu/app.jar

                    ssh -o StrictHostKeyChecking=no ubuntu@98.80.138.134 "pkill -f app.jar || true; nohup java -jar /home/ubuntu/app.jar > app.log 2>&1 &"
                    '''
                }
            }
        }

    }
}
