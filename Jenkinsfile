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
        sh 'node -v'
        }
      }
      
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
      
  }
}
