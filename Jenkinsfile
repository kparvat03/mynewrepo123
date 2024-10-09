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
               sh 'docker build -t bankingproject .'
           }
         }
         stage('port expose'){
            steps{
                sh 'docker run -d -p 8081:8081 bankingproject:latest'
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
                // Tag the Docker image with your Docker Hub repository name
                sh "docker tag bankingproject kparvat03/bankingproject:latest"
                
                // Push the tagged image to Docker Hub
                sh "docker push kparvat03/bankingproject:latest"
            }
        }
          stage ("deploy to production") {
            steps {
                ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: '/var/lib/jenkins/workspace/bankingproject/ansible-playbook.yml', vaultTmpPath: ''
            }   
       }
        
    }
}
