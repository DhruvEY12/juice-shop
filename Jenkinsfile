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

      stage('Running Jmeter') {
                  agent {
                    label 'windows-worker' // Specify the label of your Windows agent node
                    }
                  steps {
                    script { 
                        bat label: '', script: '"D:/apache-jmeter-5.6.2/apache-jmeter-5.6.2/bin/jmeter" -n -t "D:/apache-jmeter-5.6.2/apache-jmeter-5.6.2/bin/Loadtest/SDMS.jmx" -l "D:/apache-jmeter-5.6.2/apache-jmeter-5.6.2/bin/Loadtest/report.csv"'
                }
            }
        }

  }
}
