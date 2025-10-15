pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/gopinath954/Maven_Project.git'
        DEPLOY_DIR = '/opt/tomcat/webapps'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: "${GIT_REPO}"
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
    steps {
        sh '''
        sudo systemctl stop tomcat
        sudo cp target/*.war /opt/tomcat/webapps/
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
