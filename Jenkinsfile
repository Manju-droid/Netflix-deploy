pipeline{
    agent any
    stages{
        stage('deploy netflix into containers'){
            steps{
                sshagent(['client-ec2-ssh']){
                    sh ''' 
                        ssh -o StrictHostKeyChecking=no ubuntu@10.1.1.126 '
                        git clone https://github.com/Manju-droid/Netflix-deploy.git || true &&
                        cd Netflix-deploy || true &&
                        cd frontend || true &&
                        docker stop container1 || true &&
                        docker rm container1 || true &&
                        docker rmi netflix || true &&
                        docker build -t netflix . 
                        docker run -dit --name container1 -p 3000:80 netflix 
                        docker tag netflix manjunadhav/netflix-frontend-dokerfile:latest 
                        docker push manjunadhav/netflix-frontend-dokerfile:latest 
                        '
                    '''
                }
            }
        }
    }
}
