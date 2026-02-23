pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Upload to Nexus') {
            steps {
                sh 'mvn deploy'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(
                        credentialsId: 'tomcat-creds',
                        path: '',
                        url: 'http://15.206.174.223:8080'
                )],
                contextPath: 'myapp',
                war: '**/*.war'
            }
        }

    }
}
