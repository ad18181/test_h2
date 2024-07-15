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
                sh 'horusec start -p="./" --disable-docker="true" -o json --json-output-file ${WORKSPACE}/report.json'
                script {
                    env.DOCKER_WORK= "${WORKSPACE}"
                }
                sh'echo "workspace = ${DOCKER_WORK}"'
                
            }
            

        }
        
        stage('local machine ') {

            steps {
            
                sh'cat  /var/lib/jenkins/workspace/mount_test_main@2/report.json'
                sh'''
                cd /var/lib/jenkins/workspace/mount_test_main@2
                ls 
                curl -X 'POST' 'https://avantiy-pc:8443/api/v2/import-scan/'  -H 'accept: application/json' -H 'Authorization:Token ced0c0a342cb9fe4178a937abc0f446762bfc939'  -H 'Content-Type: multipart/form-data'   -H 'X-CSRFTOKEN: trDEYficxJvr5GV31dwDTGwoaAHHT4ahK4FoAPOknoQSPkgRhRodnKaRgE4oViet'   -F 'product_type_name='   -F 'active=true'   -F 'endpoint_to_add='   -F 'verified=true'   -F 'close_old_findings=false'   -F 'test_title='   -F 'engagement_name=Test1'   -F 'build_id='   -F 'deduplication_on_engagement=true'   -F 'push_to_jira=false'   -F 'minimum_severity=Info'   -F 'close_old_findings_product_scope=false'   -F 'apply_tags_to_endpoints=true'   -F 'scan_date=2024-07-11'   -F 'create_finding_groups_for_all_findings=true'   -F 'engagement_end_date=2024-07-12'   -F 'environment='   -F 'service=string'   -F 'commit_hash='   -F 'group_by=file_path'   -F 'version='   -F 'tags=string'   -F 'apply_tags_to_findings=true'   -F 'api_scan_configuration='   -F 'product_name='   -F 'file=@report.json;type=application/json'   -F 'auto_create_context=true'   -F 'lead='   -F 'scan_type=Horusec Scan'   -F 'branch_tag='   -F 'source_code_management_uri='   -F 'engagement=48' -k 
                '''
            }

        }

    }

}



