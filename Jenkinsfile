pipeline {
    agent any

    tools {
        maven 'Maven-3.9.12'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Leogabriele/java-tomcat-maven-example.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''
                dir target
                copy /Y target\\*.war "C:\\apache-tomcat-11.0.18\\webapps\\"
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deploy failed!'
        }
    }
}
