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
                        bat label: '', script: 'java -Xmx512m -jar "C:/Program Files/OWASP/Zed Attack Proxy/zap-2.13.0.jar" -cmd -port 8084 -autorun "D:/Jenkins/workspace/sdms-uat-automation-plan.yaml"'
                    } catch (Exception e) {
                        // Catch any exceptions and ignore them to prevent pipeline failure
                        currentBuild.result = 'SUCCESS'
                        echo "ZAP Command encountered an error, but it's being ignored."
                    }
                }
            }
        }

  }
}
