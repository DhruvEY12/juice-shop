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
      stage('Grype-Scan') {
        steps {
          sh 'grype dir:/var/lib/jenkins/workspace/Trial_1 -o json --scope AllLayers'
      }
    }
      stage('ZAP-Scan') {
        steps {
          sh '/usr/share/owasp-zap/zap.sh -port 6969 -cmd -quickurl https://demo.testfire.net -quickprogress -quickout /tmp/zap_scan_on_jenkins_${BUILD_ID}.html'
      }
    }
  }
}
