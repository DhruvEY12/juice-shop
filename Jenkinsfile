pipeline {
  agent any
   tools {nodejs "Nodejs14"}
    //environment {
      //SEMGREP_RULES = "p/default" 
      // SEMGREP_BRANCH = "${GIT_BRANCH}"
      //SEMGREP_BRANCH = "master"

      // Uncomment the following line to scan changed 
      // files in PRs or MRs (diff-aware scanning): 
      // SEMGREP_BASELINE_REF = "main"
    //}
    stages {
      
      stage('node version') {
        steps{
           sh '''
              node -v
              '''      
        }
      }
      
    }
      
  }

