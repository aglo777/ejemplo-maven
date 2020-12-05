pipeline {
    agent any
 tools {
    maven 'maven'
  }
    stages {
        stage('Compile') {
            steps {
                sh "mvn clean compile -e"
            }
        }
        stage('Test') {
            steps {
                sh "mvn clean test -e"
            }
        }
        stage('Package') {
            steps {
                sh "mvn clean package -e"
            }
        }
        stage('SonarQube analysis') {
                steps {
            withSonarQubeEnv(installationName:'Sonar') {
                sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
            }
          }
        }
        stage('Run') {
            steps {
                sh "mvn spring-boot:run &"
            }
        }
        stage('Test Microservice') {
            steps {
                sh "sleep 20"
                sh "curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing"
            }
        }
    }
}
