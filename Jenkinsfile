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
                    sh "docker build -t dinakar1995/hiring:o.o.2 ."
                   }
                }
           
    stage('docker push') {
          steps {
                withCredentials([string(credentialsId: 'hubPwd', variable: 'dockerhub')]) {
                     sh "docker login -u dinakar1995 -p ${dockerhub}"
                     sh "docker push dinakar1995/hiring:o.o.2"
                    }
                }
           }
      }
}
