pipeline{
    agent {
        label 'aws-agent'
    }

    stages{
        stage('build'){
            steps{
                script{
                    sh 'sudo docker build -t app-java .'
                }
            }
        }

        stage('push'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'password', usernameVariable: 'username')]) {
                        sh 'sudo docker login --username $username --password $password'
                        sh 'sudo docker tag app-java $username/app-java:latest'
                        sh 'sudo docker push $username/app-java:latest'

                    }
                }
            }
        }

        stage("deployment"){
            steps{
                script{
                    withAWS(credentials: 'aws-cli', region: 'us-east-1') {
                        sh 'aws eks update-kubeconfig --region us-east-1 --name peculiar-dubstep-monster'
                        sh 'kubectl apply -f ./k8s/deployment.yaml --validate=false'

                    }
                }
            }
        }
    }

}