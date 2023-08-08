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
      stage('Semgrep-Scan') {
        steps {
          sh 'whoami'
          sh 'semgrep scan --config auto --output scan_results.json --json'
      }
    }
      
      stage('Semgrep_result-to-DefectDojo'){
        steps {
          sh '''
          curl -X 'POST' \
          'https://defectdojo.dalmiabharat.com/api/v2/reimport-scan/' \
          -H 'accept: application/json' \
          -H 'Authorization: Token 212983a2789afcd09f252a66d83b46a8fa4a8c39' \
          -H 'Content-Type: multipart/form-data' \
          -H 'X-CSRFTOKEN: agVi7AHZPZ13PBfCOABb4yn6v12KIUNoLvf34b9vNHS0X2qig1Exvd6J0Nnkw7YO' \
          -F 'active=true' \
          -F 'do_not_reactivate=false' \
          -F 'verified=true' \
          -F 'close_old_findings=true' \
          -F 'engagement_name=Semgrep-Scan' \
          -F 'push_to_jira=false' \
          -F 'minimum_severity=Info' \
          -F 'close_old_findings_product_scope=false' \
          -F 'create_finding_groups_for_all_findings=true' \
          -F 'tags=semgrep' \
          -F 'product_name=Product-II' \
          -F 'file=@scan_results.json;type=application/json' \
          -F 'auto_create_context=true' \
          -F 'scan_type=Semgrep JSON Report' 
          '''
        }
      }
      stage('Grype-Scan') {
        steps {
          sh 'grype dir:. -o json --file grype_result.json --scope AllLayers'
      }
    }

      stage('Grype_result-to-DefectDojo'){
        steps {
          sh '''
          curl -k -X 'POST' \
          'https://defectdojo.dalmiabharat.com/api/v2/reimport-scan/' \
          -H 'accept: application/json' \
          -H 'Authorization: Token 212983a2789afcd09f252a66d83b46a8fa4a8c39' \
          -H 'Content-Type: multipart/form-data' \
          -H 'X-CSRFTOKEN: agVi7AHZPZ13PBfCOABb4yn6v12KIUNoLvf34b9vNHS0X2qig1Exvd6J0Nnkw7YO' \
          -F 'active=true' \
          -F 'do_not_reactivate=false' \
          -F 'verified=true' \
          -F 'close_old_findings=true' \
          -F 'engagement_name=Grype-scan' \
          -F 'push_to_jira=false' \
          -F 'minimum_severity=Info' \
          -F 'close_old_findings_product_scope=false' \
          -F 'create_finding_groups_for_all_findings=true' \
          -F 'tags=grype' \
          -F 'product_name=Product-II' \
          -F 'file=@grype_result.json;type=application/json' \
          -F 'auto_create_context=true' \
          -F 'scan_type=Anchore Grype' 
          '''
        }
      }
      
  }
}
