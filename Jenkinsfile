pipeline {
    agent any
        stages {
             stage('Git Checkout') {
                  steps {
                        git branch: 'main', credentialsId: 'Dinakar1995', url: 'https://github.com/Dinakar1995/hiring'
                      }
                  }
             stage( 'Maven Build') {
                  steps {
                        sh "mvn clean package"
                        }
             }
          stage('Tomcat Deploy') {
                steps {
                    sshagent(['Dinakar1995']) {
                         sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.37.20:/opt/tomcat9/webapps"
                         sh "ssh ec2-user@172.31.37.20 /opt/tomcat9/bin/shutdown.sh"
                         sh "ssh ec2-user@172.31.37.20 /opt/tomcat9/bin/startup.sh"
                   }
                }
           }
      }
}
