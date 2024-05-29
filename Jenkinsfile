pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/mvishwa16/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t tobecontinue/edurekab1:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push tobecontinue/edurekab1:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe221 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 tobecontinue/edurekab1:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 tobecontinue/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.31.152 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.31.152 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
