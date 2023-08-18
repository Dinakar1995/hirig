pipeline {
    agent any
        stages {
             stage( 'Maven Build') {
                 when {
                      branch 'develop'
                 }
                  steps {
                        sh "mvn clean package"
                        }
             }
          stage('deploy to dev') {
               when {
                      branch 'develop'
                 }
                steps {
                    sshagent(['Dinakar1995']) {
                        echo "deploying in dev"
       
                   }
                }
           }
    stage('deploy to prod') {
               when {
                      branch 'main'
                 }
                steps {
                    sshagent(['Dinakar1995']) {
                        echo "deploying in prod"
       
                   }
                }
           }
      }
}
