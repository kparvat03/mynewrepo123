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
                sh 'docker run -dt -p 8096:8096 --name c005 myimg'
            }
        }
        stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'kparvat03/admin@123', passwordVariable: 'admin@123', usernameVariable: 'kparvat03')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
        
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
