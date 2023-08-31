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
          sh '''
          pwd
          ls -lrtha
          source /home/jenkins/venv1/bin/activate 
          semgrep scan --config auto
          deactivate
          '''   
      }
    }
      
     
      stage('Grype-Scan') {
        steps {
          sh 'grype dir:. -o json --file grype_result.json --scope AllLayers'
      }
    }

      
  }
}
