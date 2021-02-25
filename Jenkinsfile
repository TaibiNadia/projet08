pipeline {
    agent { node { label 'ubuntu_slave' } }
    
    stages {
        /*stage('Test_unitaire') {
            steps {
                sh 'composer install -n'
                sh 'SYMFONY_DEPRECATIONS_HELPER=disabled composer unit-tests'
            }
        }*/
        stage('Build') {
            steps { 
                sh 'docker build -t prestashop .'
                /*sh 'docker build -f Dockerfile.db -t mysqldb .' */
            }
        }
        stage('Services') {
            steps { 
                    sh 'docker-compose up -d'
                }
        }
    
    }   
    stages {
        stage('Tests_fonctionnels') {
            wrap([$class: 'Xvfb']) {
                steps {
                    sh 'python3 ./tests-fun/funtest.py'
                }
            } 
        }
    }
        
    /*post ('Test_Results') {
            always {
                echo 'I will always execute this!'
                junit skipPublishingChecks: true, keepLongStdio: true, testResults: 'reports/*.xml' 
              
            }    
    } */ 
       
}
