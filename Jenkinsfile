pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/Sayaaliee/Project/', branch: "master"
                sh 'mvn clean package'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t sayaalieee/staragileprojectfinance:v2 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push sayaalieee/staragileprojectfinance:v2'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                    sh 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 sayaalieee/staragileprojectfinance:v2'
                    
                }
            }
        }
    }
