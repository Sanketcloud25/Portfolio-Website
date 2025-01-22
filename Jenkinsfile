pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
                sh 'rm -rf Portfolio-Website'
            }
        }
        stage('Git-Clone') {
            steps {
                sh 'git clone https://github.com/Sanketcloud25/Portfolio-Website.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                dir('Portfolio-Website') {
                    sh 'npm install'
                }
            }
        }
        stage('Build Application') {
            steps {
                dir('Portfolio-Website') {
                    sh 'npm run build'
                }
            }
        }
        stage('Copy Build to Webserver') {
            steps {
                sh 'cp -r Portfolio-Website/build/* /usr/share/nginx/html/'
            }
        }
        stage('Unzip Additional Files') {
            steps {
                dir('Portfolio-Website') {
                    sh 'unzip 3.93.25.110.zip'
                }
            }
        }
        stage('Configure SSL Certificates') {
            steps {
                sh 'sudo cat Portfolio-Website/certificate.crt Portfolio-Website/ca_bundle.crt >> /var/lib/jenkins/certificate.crt'
            }
        }
        stage('move private key') {
            steps {
                sh 'sudo mv Portfolio-Website/private.key /var/lib/jenkins/private.key'
            }
        }
        stage('Update Nginx Configuration') {
            steps {
                sh 'sudo mv Portfolio-Website/nginx.conf /etc/nginx/nginx.conf'
            }
        }
        stage('Restart Nginx') {
            steps {
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}
