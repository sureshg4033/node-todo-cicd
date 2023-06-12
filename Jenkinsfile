pipeline{
    agent{label 'agent1'}
    stages{
        stage('code clone'){
            steps{
                git url:'https://github.com/sureshg4033/node-todo-cicd.git', branch: 'development'
            }
        }
        stage('build and test' ){
            steps{
              sh 'docker build . -t sureshg4033/node-todo-cicd-app:latest'
            }
        }
       stage('deploy'){
            steps{
              sh 'docker-compose down && docker-compose up -d'
}
}
}
}
