pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/kparvat03/mynewrepo123/'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with priyanka'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with priyanka'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa with priyanka'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package with priyanka'){
            steps{
                sh 'mvn package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t myimg .'
           }
         }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 8097:8097 --name c006 myimg'
            }
        }
        
        stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                }
            }
        }
    
          stage("docker tag & push"){
            steps {
                sh "docker tag myimg bankingproject/myimg:latest"
                sh 'docker push bankingproject/myimg:latest'
                   }
        }
        
    }
}
