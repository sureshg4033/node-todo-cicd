pipeline{
    agent{label 'developer'}
    stages{
        stage('code clone'){
            steps{
                git url:'https://github.com/dhiyani12/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build and test' ){
            steps{
              sh 'docker build . -t shubhamdhyani/node-todo-cicd-app:latest'
            }
        }
        stage('login & push' ){
           steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
        	     sh 'docker push shubhamdhyani/node-todo-cicd-app:latest'
               }
               }
        }
       stage('deploy'){
            steps{
              sh 'docker-compose down && docker-compose up -d'
}
}
}
}
