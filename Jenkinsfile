pipeline {
    agent any
    // {
    //     docker {
    //         image 'tomcat:8.5.51'
    //         args '-u root -p 7070:8080 -v ./webapp/target/*.war:/usr/local/tomcat/webapps/'
    //     }
    // }

    tools {
    maven 'localMaven'
    }

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
                // sh "/usr/local/bin/docker build -t tomcat-docker-webapp:${env.BUILD_ID} ."
                sh "docker build -t tomcat-docker-webapp:${env.BUILD_ID} ."
            }
        }

    }
}