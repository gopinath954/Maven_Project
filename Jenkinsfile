pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/yourusername/java-web-app.git'
        DEPLOY_DIR = '/opt/tomcat/webapps'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "${GIT_REPO}"
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying WAR to Tomcat...'
                sh '''
                sudo systemctl stop tomcat
                sudo cp target/*.war ${DEPLOY_DIR}/app.war
                sudo systemctl start tomcat
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
