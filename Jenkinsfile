pipeline{
    agent any
    tools{
        maven "maven-3.9"
    }
    stages{
        stage("SCM checkout"){
            steps{
                checkout scm
            }
        }
        stage("Build"){
            steps{
                sh "mvn clean package"
            }
        }
    }
}
