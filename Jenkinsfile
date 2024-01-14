pipeline {
    agent any

    stages {
        stage('Push Docker image to ECR') {
            steps {
                script {
                    // Authenticate Docker with ECR
                    sh "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 381492160554.dkr.ecr.ap-south-1.amazonaws.com"

                    // Build Docker image
                    sh "docker build -t tech ."

                    // Tag Docker image
                    sh "docker tag tech:latest 381492160554.dkr.ecr.ap-south-1.amazonaws.com/tech:latest"

                    // Push Docker image to ECR
                    sh "docker push 381492160554.dkr.ecr.ap-south-1.amazonaws.com/tech:latest"
                }
            }
        }
//tech
        stage('Pull Docker image from ECR') {
            steps {
                script {
                    // Pull Docker image from ECR
                    sh "docker pull 381492160554.dkr.ecr.ap-south-1.amazonaws.com/tech:latest"

                    // Remove existing container if it exists
                    sh 'docker container ls -a -f name=My-practice-website-client -q | xargs -r docker container rm -f'

                    // Run Docker container
                    sh "docker run -itd --name My-practice-website-client -p 4200:80 381492160554.dkr.ecr.ap-south-1.amazonaws.com/tech:latest"
                    // You may add additional Docker run options or environment variables as needed
                    // sh "docker run -itd  -p 4200:80 --name My-practice-website-client  ng serve --host 0.0.0.0"
                }
            }
        }
    }
}
