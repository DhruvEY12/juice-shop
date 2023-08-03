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
          sh 'semgrep scan --config auto'
      }
    }
      stage('Scan') {
        steps {
          sh 'grype dir:/var/lib/jenkins/workspace/Combine_1 -o json --scope AllLayers'
      }
    }
  }
}
