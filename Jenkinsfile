pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit:'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    environment{
        def appVersion = '' //variable declaration
         nexus_url = 'nexus.sdevops.cloud:8081'
    }
  
    stages {
        stage('read the version'){
            steps{
                script{
                    def packagejson = readJSON file: 'package.json'
                    appVersion = packagejson.version
                    echo "application version: $appVersion"
                }
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
        stage('Build') {
            steps {
                sh """
                zip -q -r backend-${appVersion}.zip * -x jenkinsfile -x backend-${appVersion}.zip
                ls -ltr
             
                """
            }
        }
           stage('Nexus Artifact uploader') {
            steps {
                 script{
                        nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: "${nexusUrl}",
                        groupId: 'com.expense',
                        version: "${appVersion}",
                        repository: "backend",
                        credentialsId: 'nexus-auth',
                        artifacts: [
                            [artifactId: "backend" ,
                            classifier: '',
                            file: "backend-" + "${appVersion}" + '.zip',
                            type: 'zip']
                        ]
                    )
                }
            }
        }

        stage('Deploy'){
            steps{
                script{
                    def params = [
                        string(name: 'appVersion', value: "${appVersion}")
                        ]
                        build job : "backend-deploy", parameters: params, wait : false
                    
                }
            }
        }


               
    }
          
    post{
        always{
            echo " i will always say hellow again"
            //deleteDir()
        }
        success{
            echo " i will run when pipeline is success"
        }
        failure{
            echo " i will run when pipeline is failure"
        }
    }
}
