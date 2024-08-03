pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit:'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
  
    stages {
        stage('install dependencies') {
            steps {
                sh """
                npm install
                ls -ltr
                """
            }
        }
               
    }
          
    post{
        always{
            echo " i will always say hellow again"
            deleteDir()
        }
        success{
            echo " i will run when pipeline is success"
        }
        failure{
            echo " i will run when pipeline is failure"
        }
    }
}
