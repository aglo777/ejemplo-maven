pipeline {
    agent any
 tools {
    maven 'maven'
  }
    stages {
        stage('Compile') {
            steps {
                dir("/Users/angelocossio/Downloads/ejemplo-maven"){
                    sh "mvn clean compile -e"
                }
            }
        }
        stage('Test') {
            steps {
                dir("/Users/angelocossio/Downloads/ejemplo-maven"){
                sh "mvn clean test -e"
                }
            }
        }
        stage('Package') {
            steps {
                dir("/Users/angelocossio/Downloads/ejemplo-maven"){
                sh "mvn clean package -e"
                }
            }
        }
        stage('Run') {
            steps {
                dir("/Users/angelocossio/Downloads/ejemplo-maven"){
                sh "mvn spring-boot:run &"
                }
            }
        }
        stage('Test Microservice') {
            steps {
                dir("/Users/angelocossio/Downloads/ejemplo-maven"){
                sh "sleep 20"
                sh "curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing"
                }
            }
        }
    }
}

