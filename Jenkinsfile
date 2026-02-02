pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    environment {
        TOMCAT_URL = 'http://localhost:8080'
        TOMCAT_CREDENTIALS = credentials('tomcat-creds')
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/daticahealth/java-tomcat-maven-example.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh """
                curl -u $TOMCAT_CREDENTIALS_USR:$TOMCAT_CREDENTIALS_PSW \
                -T target/*.war \
                $TOMCAT_URL/manager/text/deploy?path=/demoapp&update=true
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build or deploy failed!'
        }
    }
}
