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
      stage('DAST-Scanning') {
            parallel {
                stage('PD-Nuclei') {
                    steps {
                        sh '''
                        source ~/.bashrc
                        nuclei -u https://demo.testfire.net/ -nc
                        '''   
                    }
                }
                stage('ZAP') {
                    steps {
                        sh '/usr/share/owasp-zap/zap.sh -port 6969 -cmd -quickurl https://demo.testfire.net -quickprogress -quickout /tmp/zap_scan_on_jenkins.xml'
                        // Add commands to run integration tests
                    }
                }
            }
        }
     
      
  }
}
