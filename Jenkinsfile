pipeline {
    agent any


    tools {
    maven 'localMaven'
    }

    parameters {
        string(name: 'tomcat_dev', defaultValue: '54.80.138.56', description: 'Staging server')
        string(name: 'tomcat_prod', defaultValue: '3.223.192.101', description: 'Production server')
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
                        sh "scp -i /Users/lenz/.ssh/testkey.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i /Users/lenz/.ssh/testkey.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat/webapps"
                    }
                }
            }
        }
    }
}
