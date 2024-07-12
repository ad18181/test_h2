pipeline {

    agent {

        docker {image 'horuszup/horusec-cli:alpha'}
    }

 

    stages {

        stage('Checkout') {

            steps {

                // Checkout code from the branch

                checkout scm

            }

        }

 

        stage('Code Analysis with Horusec') {

            agent {
            
                docker { image 'horuszup/horusec-cli:alpha' }
            
            } 
            
            steps {
            
                sh 'horusec start -p="./" --disable-docker="true" --config-file-path=horusec-config.json '
                sh'pwd'
            }

        }
        
        stage('local machine ') {

            agent any 
                
            
            steps {
            
                sh'pwd'
                
            }

        }

    }

}



