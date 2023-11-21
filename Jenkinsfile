pipeline {
  agent any
    //environment {
      //SEMGREP_RULES = "p/default" 
      // SEMGREP_BRANCH = "${GIT_BRANCH}"
      //SEMGREP_BRANCH = "master"

      // Uncomment the following line to scan changed 
      // files in PRs or MRs (diff-aware scanning): 
      // SEMGREP_BASELINE_REF = "main"
    //}
    stages {
      stage('SAST-Scanning') {
            parallel {
                stage('semgrep') {
                    steps {
                       sh '''
                       pwd
                       ls -lrtha
                       source /home/jenkins/venv1/bin/activate 
                       semgrep scan --config auto --output Semgrep_results.json --json
                       deactivate
                       '''   
                    }
                }

                stage('Grype') {
                    steps {
                        sh 'grype dir:. -o json --file grype_result.json --scope AllLayers'
            
                    }
                }
              
            }
        
        }
      stage('Semgrep_result-to-DefectDojo'){
        steps {
          script {
                       sh "curl -X 'POST' \
                        'https://defectdojo.dalmiabharat.com/api/v2/reimport-scan/' \
                        -H 'accept: application/json' \
                        -H 'Authorization: Token ${DefectDojo-Authorization}' \
                        -H 'Content-Type: multipart/form-data' \
                        -H 'X-CSRFTOKEN: ${DefectDojo X-CSRFTOKEN}' \
                        -F 'active=true' \
                        -F 'do_not_reactivate=false' \
                        -F 'verified=true' \
                        -F 'close_old_findings=true' \
                        -F 'engagement_name=Scanning' \
                        -F 'push_to_jira=false' \
                        -F 'minimum_severity=Info' \
                        -F 'close_old_findings_product_scope=false' \
                        -F 'create_finding_groups_for_all_findings=true' \
                        -F 'product_name=Trial' \
                        -F 'file=@Semgrep_results.json;type=application/json' \
                        -F 'auto_create_context=true' \
                        -F 'scan_type=Semgrep JSON Report'"
                    }
        }
      }

       stage('grype_result-to-DefectDojo'){
        steps {
          script {
                       sh "curl -X 'POST' \
                        'https://defectdojo.dalmiabharat.com/api/v2/reimport-scan/' \
                        -H 'accept: application/json' \
                        -H 'Authorization: Token 212983a2789afcd09f252a66d83b46a8fa4a8c39' \
                        -H 'Content-Type: multipart/form-data' \
                        -H 'X-CSRFTOKEN: agVi7AHZPZ13PBfCOABb4yn6v12KIUNoLvf34b9vNHS0X2qig1Exvd6J0Nnkw7YO' \
                        -F 'active=true' \
                        -F 'do_not_reactivate=false' \
                        -F 'verified=true' \
                        -F 'close_old_findings=true' \
                        -F 'engagement_name=Scanning' \
                        -F 'push_to_jira=false' \
                        -F 'minimum_severity=Info' \
                        -F 'close_old_findings_product_scope=false' \
                        -F 'create_finding_groups_for_all_findings=true' \
                        -F 'product_name=Trial' \
                        -F 'file=@grype_result.json;type=application/json' \
                        -F 'auto_create_context=true' \
                        -F 'scan_type=Anchore Grype'"
                    }
        }
      }
      
  }
}
