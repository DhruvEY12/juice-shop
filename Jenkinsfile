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
                stage('ZAP') {
                    steps {
                        sh '/usr/share/owasp-zap/zap.sh -port 6969 -cmd -quickurl https://demo.testfire.net -quickprogress -quickout /tmp/zap_scan_on_jenkins.xml'
                        // Add commands to run integration tests
                    }
                }

                stage('PD-Nuclei') {
                    steps {
                        sh '''
                        source ~/.bashrc
                        nuclei -u https://demo.testfire.net/ -nc
                        '''   
                    }
                }
              
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
                       semgrep scan --config auto
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
