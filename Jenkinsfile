pipeline {

    agent any

    tools {
        maven 'maven-3.9'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code already checked out by Jenkins'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

    }
}
