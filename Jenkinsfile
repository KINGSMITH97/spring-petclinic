pipeline{
    agent any 

    tools{
        maven 'maven3.9.9'
    }
    stages{

        stage('Git checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/KINGSMITH97/spring-petclinic.git'
            }
        }

        stage('Build with maven'){
            steps{
                sh "mvn clean"
            }
        }

        stage('package with maven'){
            steps{
                sh "mvn package"
            }
        }
    }
    post{
        success {
            slackSend(channel: '#shopper', color: 'good', message: "Build SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        }
        failure {
            slackSend(channel: '#shopper', color: 'danger', message: "Build FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        }
        always {
            slackSend(channel: '#shopper', color: 'warning', message: "Build Completed: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        }
    }

}