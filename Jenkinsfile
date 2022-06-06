pipeline {
    agent none

    stages {
        stage('Install Dependencies...') {
            agent {
                label 'node_dev1'
            }
            steps {
                echo 'Installing APP Dependencies...'
                sh 'npm install'
                sh 'npm install -D sonarqube-scanner'
            }
        }
        stage('Execute Unit Test...') {
            agent {
                label 'node_dev1'
            }
            steps {
                echo 'Running Unit Test... npm test'
            }
        }
        stage('Execute Sonar Scanner...') {
            agent {
                label 'node_dev1'
            }
            steps {
                sh 'npm run sonar'
            }
        }
        stage('Build Application...') {
            agent {
                label 'node_dev1'
            }
            steps {
                echo 'Building Application...'
                sh 'ng build'
        }   }
        stage('Compressing Application Files...') {
            agent {
                label 'node_dev1'
            }
            steps {
                echo 'Compressing Application...'
                sh 'cp /home/administrator/proyects/angular_app/webapp/workspace/angular_app_main/dist/web_angular/*.* ~/application/'
                sh 'cd ~/application/'
                sh 'zip -r application.zip *'

            }
        }
        stage('Copying artifacts to Docker Host Container...') {
            agent {
                label 'node_dev1'
            }
            steps {
                echo 'Building Application...'
                sh 'sshpass -p G@p53rv3r scp /home/administrator/proyects/angular_app/webapp/workspace/angular_app_main/dist/application.zip administrator@172.16.1.111:/home/administrator/proyects/angular_ci-cd/src'
            }
        }
        stage('Deploy Web Application...') {
            agent {
                label 'docker_host'
            }
            steps {
                echo 'Deploying Web Application...'
                sh 'cd /home/administrator/proyects/angular_ci-cd/src'
                sh 'unzip application.zip'
                
                
            }
        }
    }
}
