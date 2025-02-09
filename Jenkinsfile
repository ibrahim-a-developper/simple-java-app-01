pipeline{
    agent {
        label 'aws-agent'
    }
    stages{
        stage('Build'){
            steps{
                   sh 'mvn clean package'

            }
        }

        stage('Test'){
            steps{
                   echo 'Test'

            }
        }
    }

    post {
    success {

        slackSend channel: '#jenkins-ci', message: "Build Success - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'softtechgroupe', tokenCredentialId: 'slack-notification'
        }

    failure {
        slackSend channel: '#jenkins-ci', message: "Build Failed - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'softtechgroupe', tokenCredentialId: 'slack-notification'


        }
    }
}