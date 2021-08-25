pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'oktbabs', url: 'https://github.com/oktbabs/mycicdpipeline.git'
            }
        }
        stage('Install ansible trial') {
            steps {
                sh 'sudo yum -y update'
                sh 'sudo yum -y install ansible'
            }
        }
    }
}
