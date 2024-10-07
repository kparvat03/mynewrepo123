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
                sh 'docker run -dt -p 8094:8094 --name c002 myimg'
            }
        }   
    }
}
