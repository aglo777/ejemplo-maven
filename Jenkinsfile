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
        stage('Upload Nexus') {
            steps {
                nexusPublisher nexusInstanceId: 'Nexus', nexusRepositoryId: 'test-repo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: 'jar', filePath: '/Users/angelocossio/Downloads/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
            }
        }
    }
}
 