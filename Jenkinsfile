pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'oktbabs', url: 'https://github.com/oktbabs/mycicdpipeline.git'
            }
        }
        stage('Setup and Synchronise time') {
            steps {
                sh 'sudo systemctl stop ntp'
                sh 'sudo ntpdate -qu 0.debian.pool.ntp.org'
                sh 'sudo systemctl restart ntp'
                sh 'sudo systemctl status ntp'
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
