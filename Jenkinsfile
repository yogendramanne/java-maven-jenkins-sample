pipeline {
    agent any

    tools {
        maven 'Maven 3.8.5'   // Set this name in Jenkins > Global Tool Config
        jdk 'JDK 11'          // Also configure this in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/yogendramanne/java-maven-jenkins-sample.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            echo 'Build and tests successful!'
        }
        failure {
            echo 'Something failed. Check logs.'
        }
    }
}

