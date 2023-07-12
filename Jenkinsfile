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
    stage('Grype-Build')
    {
      steps
      {
        grypeScan scanDest: 'dir:/tmp', repName: 'myScanResult.txt', autoInstall: 0
      }
    }
  }
}
