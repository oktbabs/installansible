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
         stage('Carrying out Unit Tests') {
            steps {
                sh '/home/jenkins/apache-jmeter-5.4.1/bin/jmeter -j jmeter.save.saveservice.output_format=xml -n -t /home/jenkins/apache-jmeter-5.4.1/bin/Jenkins_Test_Plan.jmx -l /home/jenkins/apache-jmeter-5.4.1/jenkins.io.report.jtl'
            }
        }
    }
}
