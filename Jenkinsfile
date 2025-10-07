pipeline {
    agent any

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/pa1087/Project1.git'
                slackSend channel: 'jenkinbuilds', message: 'Got the code from GitHub successfully'
            }
        }

        stage('Perform Build') {
            steps {
                sh 'mvn package'
                slackSend channel: 'jenkinbuilds', message: 'Build done using Maven successfully'
            }
        }

        stage('Deploy to Test') {
            steps {
                deploy adapters: [tomcat9(
                    alternativeDeploymentContext: '', 
                    credentialsId: 'tomcat', 
                    path: '', 
                    url: 'http://10.3.15.131:8080'
                )], 
                contextPath: 'myapp', 
                war: '**/*.war'
                
                slackSend channel: 'jenkinbuilds', message: 'Deployed successfully at http://184.72.115.51:8080/myapp'
            }
        }
    }
}
