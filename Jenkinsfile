pipeline{
    agent {label 'dev'}
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/Vivek9120/node-todo-cicd.git', branch:'master'
                
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t vk84178/node-todo:latest' 
            }


        }

        stage('pushing to dockerhub'){
            steps{
                echo "Logging in and pushing to docker hub "
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubPassword',usernameVariable:'dockerhubUser')]){
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}  "
                    sh "docker push vk84178/node-todo:latest "
                }
            }
        }
        stage('Depolying'){
            steps{
                sh 'docker-compose down && docker-compose up -d '
                
            }
        }
    }
}
