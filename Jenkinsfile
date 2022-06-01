pipeline {
    agent {
        label 'node_dev1'
    }

    stages {
        stage('Install Dependencies...') {
            steps {
                echo 'Installing APP Dependencies...'
                sh 'npm install'
            }
        }
        stage('Execute Unit Test...') {
            steps {
                echo 'Running Unit Test... npm test'
            }
        }
        stage('Build Application...') {
            steps {
                echo 'Building Application...'
                sh 'ng build'
            }
        }
    }
}
