pipeline {

    agent any 
   
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
            
                sh 'horusec start -p="./" --disable-docker="true" -o json '
                sh'pwd'
            }

        }
        
        stage('local machine ') {

            steps {
            
                sh'pwd'
                
            }

        }

    }

}



