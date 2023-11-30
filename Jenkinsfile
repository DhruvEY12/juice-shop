pipeline {
  agent any
    environment {
      SEMGREP_RULES = "p/default" 
      // SEMGREP_BRANCH = "${GIT_BRANCH}"
      SEMGREP_BRANCH = "master"

      // Uncomment the following line to scan changed 
      // files in PRs or MRs (diff-aware scanning): 
      // SEMGREP_BASELINE_REF = "main"
    }
    stages {
      stage('Execute ZAP Command on Windows') {
                  agent {
                    label 'windows-worker' // Specify the label of your Windows agent node
                    }
                  steps {
                    script {
                      try {
                        bat label: '', script: 'java -Xmx512m -jar "C:/Program Files/OWASP/Zed Attack Proxy/zap-2.13.0.jar" -cmd -port 8084 -autorun "D:/API/Suvidha/Trial.yaml"'
                    } catch (Exception e) {
                        // Catch any exceptions and ignore them to prevent pipeline failure
                        currentBuild.result = 'SUCCESS'
                        echo "ZAP Command encountered an error, but it's being ignored."
                    }
                }
            }
        }

      stage('ZAP_result-to-DefectDojo'){
              agent {
                label 'windows-worker' // Specify the label of your Windows agent node
            }
        steps {
          script {
bat '''curl -X "POST" \
"https://defectdojo.dalmiabharat.com/api/v2/reimport-scan/" \
-H "accept: application/json" \
-H "Authorization: Token 212983a2789afcd09f252a66d83b46a8fa4a8c39" \
-H "Content-Type: multipart/form-data" \
-H "X-CSRFTOKEN: jzYVKdBeRO4mX1hrQ5u7N1nmAmU5tzrAUOiGHO3KPwVj5ss7iwxteG6Z58fFhMC0" \
-F "active=true" \
-F "do_not_reactivate=false" \
-F "verified=true" \
-F "close_old_findings=true" \
-F "engagement_name=Scanning" \
-F "push_to_jira=false" \
-F "minimum_severity=Info" \
-F "close_old_findings_product_scope=false" \
-F "create_finding_groups_for_all_findings=true" \
-F "tags=zap" \
-F "product_name=Trial" \
-F "file=@ZAP-Report.xml;type=text/xml" \
-F "auto_create_context=true" \
-F "scan_type=ZAP Scan"'''
                    }
        }
      }

  }
}
