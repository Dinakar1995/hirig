pipeline {
    agent any
        stages {
             stage( 'Maven Build') {
                  steps {
                        sh "mvn clean package"
                        }
             }
          stage('Dokcer Build') {
                steps {
                    sh "docker build -t dinakar1995/hiring:${commit_id()} ."
                   }
                }
           
    stage('docker push') {
          steps {
                withCredentials([string(credentialsId: 'hubPwd', variable: 'dockerhub')]) {
                     sh "docker login -u dinakar1995 -p ${dockerhub}"
                     sh "docker push dinakar1995/hiring:${commit_id()}"
                    }
                }
           }
    stage('Tomcat Deploy') {
          steps {
                sshagent(['Dinakar1995']) {
	        sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.35.199 docker rm -f hiring"    
                sh "ssh ec2-user@172.31.35.199 docker run -d -p 8080:8080 --name hiring dinakar1995/hiring:${commit_id()}"
                      } 
                    }
                }
           }
      
      }
def commit_id(){
    id = sh returnStdout: true, script: 'git rev-parse HEAD'
    return id
}
