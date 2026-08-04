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
                sh 'mvn clean package'
            }
        }
        stage("SonarQube Analysis"){
            steps{
                withSonarQubeEnv('SonarQube'){
                    sh '''
                    mvn org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                    -Dsonar.projectKey=jenkins-demo \
                    -Dsonar.projectName=jenkins-demo
                    '''
                }
            }
        }
    }
}
