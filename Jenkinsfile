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
            
                docker { 
                    image 'horuszup/horusec-cli:alpha' 
                    args '-v /home/amogh.dixit/Projects/mount:/mount:rw,z'
                }
            
            } 
            
            steps {
            
                sh'cd /mount'
                sh 'horusec start -p="./" --disable-docker="true" --config-file-path=horusec-config.json'
                
            }

        }
        
        stage('local machine ') {

            steps {
            
                sh'cat  /var/lib/jenkins/workspace/mount_test_main@2/report.json'
                
            }

        }

    }

}



