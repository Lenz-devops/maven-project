pipeline {
    agent {
        docker {
            image 'tomcat:8.5.51'
            args '-u root -p 7070:8080 -v ./webapp/target/*.war:/usr/local/tomcat/webapps/'
        }
    }

    tools {
    maven 'localMaven'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
                //sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
        }

    }
}