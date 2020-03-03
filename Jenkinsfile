pipeline {
    agent 
    {
        docker {
            image 'tomcat:8.5.51'
            args '-u root -p 7072:8080 -v ./webapp/target/*.war:/usr/local/tomcat/webapps/'
        }
    }

    tools {
    maven 'localMaven'
    }

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building package'
                sh 'mvn clean package'
                echo 'building docker image'
                sh "/usr/local/bin/docker build -t tomcat-docker-webapp:${env.BUILD_ID} ."
                echo 'running docker image'
                sh "/usr/local/bin/docker container run -it -d --name jenkins-test-${env.BUILD_ID} -p 90${env.BUILD_ID}:8080 tomcat-docker-webapp:${env.BUILD_ID}"
 
            }
        }

    }
}