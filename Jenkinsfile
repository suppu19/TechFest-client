pipeline {
    agent any
environment {
         AWS_ACCESS_KEY_ID     = 'AKIAVRUVUNAVOI4RF25T'
         AWS_SECRET_ACCESS_KEY = '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'
         AWS_REGION = 'us-east-1'
        // LOG_GROUP_NAME = 'practice'
         // LOG_STREAM_NAME = '${BUILD_NAME}-${BUILD_NUMBER}'
     }
    stages {
        stage('Push Docker image to ECR') {
            steps {
                script {
                    // Authenticate Docker with ECR
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 381492160554.dkr.ecr.us-east-1.amazonaws.com"
                    // Build Docker image
                    sh "docker build -t tech-feast ."

                    // Tag Docker image
                    sh "docker tag tech-feast:latest 381492160554.dkr.ecr.us-east-1.amazonaws.com/tech-feast:latest"

                    // Push Docker image to ECR
                    sh "docker push 381492160554.dkr.ecr.us-east-1.amazonaws.com/tech-feast:latest"
                }
            }
        }
//tech
        stage('Pull Docker image from ECR') {
            steps {
                script {
                    // Pull Docker image from ECR
                    sh "docker pull 381492160554.dkr.ecr.us-east-1.amazonaws.com/tech-feast:latest"

                    // Remove existing container if it exists
                    sh 'docker container ls -a -f name=My-practice-website-client -q | xargs -r docker container rm -f'

                    // Run Docker container
                    sh "docker run -itd --name My-practice-website-client -p 4200:80 381492160554.dkr.ecr.us-east-1.amazonaws.com/tech-feast:latest"
                    // You may add additional Docker run options or environment variables as needed
                    // sh "docker run -itd  -p 4200:80 --name My-practice-website-client  ng serve --host 0.0.0.0"
                }
            }
        }
    }
}
