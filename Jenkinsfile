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
