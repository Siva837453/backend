pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit:'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters{
        choice(name: 'action', choices:['Apply', 'Destroy'], description: 'Pick something')
    }

  
    stages {
        stage('init') {
            steps {
                sh """
                 echo "Hi this is testing"
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
