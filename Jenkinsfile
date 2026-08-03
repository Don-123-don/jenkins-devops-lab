pipeline {

    agent any

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
