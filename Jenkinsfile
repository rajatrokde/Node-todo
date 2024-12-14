pipeline{
    agent {label 'dev-agent'}
    stages{
        stage('Code'){
            steps{
                git url:'https://github.com/nahidkishore/node-todo-cicd.git', branch:'master'
                
            }
        }
        stage('Build and Test'){
            steps{
                sh "docker build . -t node-todo-app-cicd"

                
            }
        }
         stage("Push to Docker Hub"){
               steps{
                   
                echo 'login into docker hub and pushing image....'
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]){
                     
                     sh "docker tag node-todo-app-cicd ${env.dockerHubUser}/node-todo-app-cicd:latest"
                     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                     sh "docker push ${env.dockerHubUser}/node-todo-app-cicd:latest"


               }
           }
         }
           
        stage('Deploy'){
            steps{
                echo "Deploying...."
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}




// pipeline {
//     agent { label 'node-agent' }
    
//     stages{
//         stage('Code'){
//             steps{
//                 git url: 'https://github.com/LondheShubham153/node-todo-cicd.git', branch: 'master' 
//             }
//         }
//         stage('Build and Test'){
//             steps{
//                 sh 'docker build . -t trainwithshubham/node-todo-test:latest'
//             }
//         }
//         stage('Push'){
//             steps{
//                 withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
//         	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
//                  sh 'docker push trainwithshubham/node-todo-test:latest'
//                 }
//             }
//         }
//         stage('Deploy'){
//             steps{
//                 sh "docker-compose down && docker-compose up -d"
//             }
//         }
//     }
// }
