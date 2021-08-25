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
                  sh 'sudo yum install ntp ntpdate -y'
                  sh 'sudo systemctl start ntpd'
                  sh 'sudo systemctl enable ntpd'
                  sh 'sudo systemctl status ntpd'
                  sh 'sudo ntpdate -u -s 0.centos.pool.ntp.org 1.centos.pool.ntp.org 2.centos.pool.ntp.org'
                  sh 'sudo systemctl restart ntpd'
                  sh 'sudo timedatectl'
                  sh 'sudo hwclock -w'
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
           stage('Publishing Unit Tests Results') {
            steps {
                sh 'cat /home/jenkins/apache-jmeter-5.4.1/jenkins.io.report.jtl'
            }
        }
          stage('Email my information') {
            steps {
               emailext body: '''Dear Buddy, Your pipeline executed with no issues''', 
               subject: 'Your pipeline has been completed', 
               to: 'oktbabs@gmail.com'
            }
        }
    }
}
