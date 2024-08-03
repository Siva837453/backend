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
        stage('read the version'){
            steps{
                def packagejson = readJson file: 'package.json'
                def appVersion = packagejson.version
                echo "application version: $appVersion"
            }
        }
        stage('install dependencies') {
            steps {
                sh """
                npm install
                ls -ltr
                echo "application version: $appVersion"
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
