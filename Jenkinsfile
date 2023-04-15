pipeline{
    agent any 
    stages{
        stage('1-git clone'){
            steps{
                checkout scmGit(branches: [[name: '(main|develop|feature.*)']], extensions: [], userRemoteConfigs: [[credentialsId: 'maestrog-id', url: 'https://github.com/maestroghub/multibranchrepo2.git']])
            }
        }
        stage('2 system-resources-check'){
            steps{
                sh 'lsblk'
                sh 'lscpu'
                sh 'date'
            }
        }
        stage('parallel sub-job1'){
            parallel{
                stage('disk-check'){
                    steps{
                        sh 'free-g'
                    }
                }
            }
        }
        stage('3 system-availability-check'){
            steps{
                sh 'uptime'
            }
        }
        stage('4 os assessment'){
            steps{
                sh 'cat /etc/os-release'
            }
        }
        stage('parallel sub-job2'){
            parallel{
                stage('disk-check 2'){
                    steps{
                        sh 'free -m'
                    }
                }
            }
        }
        stage('code deploy'){
            when{
                branch 'develop'{
                    steps{
                        sh 'id jenkins'
                        sh 'sudo systemctl status jenkins'
                    }  
                }
            }
        }
    }
}
