pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '54.255.180.55:8090', description: 'Staging Server')
         
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
					
                        sh "cp -i **/target/*.war /home/ec2-user/apache-tomcat-8.5.40/webapps"
                    }
                }
                }
            }
        }
    }