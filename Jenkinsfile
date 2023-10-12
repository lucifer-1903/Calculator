pipeline{
    agent any
    stages{
        stage("Code"){
            steps{
                echo "Code cloned"
                git url:'https://github.com/lucifer-1903/Calculator.git',
                branch:'Master'
            }
        }
        stage("Build"){
            steps{
                sh "docker build . -t notes-app"
            }
        }
        stage("Pushing to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"docker-hub-credentials",passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]){
                sh "docker tag notes-app ${env.DOCKER_USERNAME}/notes-app:latest"
                sh "docker login -u ${env.DOCKER_USERNAME} -p ${env.DOCKER_PASSWORD}"
                sh "docker push ${env.DOCKER_USERNAME}/notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "deploy"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
