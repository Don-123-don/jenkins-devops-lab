pipeline{
    agent any
    parameters{
        string{
            name : "APP_VERSION",
            defaultValue : '1.0.0',
            description : 'Application Version'
        }
        choice{
            name : 'ENVIRONMENT',
            choices : ['Dev','QAT','PRD'],
            description : 'Select Environment'
        }
        booleanParam{
            name : 'DEPLOY',
            defaultValue : false,
            description : 'Deploy after build?'
        }
    }
    tools{
        maven "maven-3.9"
    }
    environment{
        Build_CMD = "clean package"
    }
    stages{
        stage("SCM checkout"){
            steps{
                checkout scm
            }
        }
        stage("Build"){
            steps{
                sh "mvn ${Build_CMD}"
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
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage("Environments"){
            steps{
                echo "Build = ${env.BUILD_NUMBER}"
                echo "Workspace = ${env.WORKSPACE}"
                echo "Job Name = ${env.JOB_NAME}"
            }
        }

    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
        always {
            echo 'Pipeline finished.'
        }
    }

}
