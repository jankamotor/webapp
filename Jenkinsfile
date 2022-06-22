pipeline {
    agent none

    stages {
        stage('Installing Dependencies...') {
            agent {
                label 'node_dev1'
            }
            steps {
                sh 'npm install'
                sh 'npm install -D sonarqube-scanner'
            }
        }
        stage('Executing Lint Test...') {
            agent {
                label 'node_dev1'
            }
            steps {
                sh 'npm run lint'
            }
        }
        stage('Executing Unit Test...') {
            agent {
                label 'node_dev1'
            }
            steps {
                sh 'npm run test'
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
                sh 'cp /home/administrator/proyects/angular_app/webapp/workspace/angular_app_main/dist/web_angular/*.* ~/application/'
                //sh 'tar cvjf application.tar.bz2 /home/administrator/application/*.*'
            }
        }
        stage('Initializing Web Server...') {
            agent {
                label 'docker_host'
            }
            steps {
                dir ('/home/administrator/proyects/angular_ci-cd') {
                sh 'docker-compose build'
                sh 'docker-compose up -d --no-color --wait'
                sh 'docker-compose ps'
                
               }
                  
            }
        }
        stage('Deploying Application...') {
            agent {
                label 'docker_host'
            }
            steps {
                sh 'sshpass -p G@p53rv3r scp administrator@172.16.1.108:~/application/*.* /home/administrator/proyects/angular_ci-cd/src'
                  
            }
        }
    }
}
