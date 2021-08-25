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
                  sh 'yum install ntp ntpdate -y'
                  sh 'systemctl start ntpd'
                  sh 'systemctl enable ntpd'
                  sh 'systemctl status ntpd'
                  sh 'ntpdate -u -s 0.centos.pool.ntp.org 1.centos.pool.ntp.org 2.centos.pool.ntp.org'
                  sh 'systemctl restart ntpd'
                  sh 'timedatectl'
                  sh 'hwclock -w'
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
           stage('Carrying out Unit Tests') {
            steps {
                sh '/home/jenkins/apache-jmeter-5.4.1/jenkins.io.report.jtl'
            }
        }
    }
}
