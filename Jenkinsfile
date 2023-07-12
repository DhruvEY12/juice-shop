pipeline
{
  agent any
  options
  {
    skipStagesAfterUnstable()
  }
  stages
  {
    stage('Build')
    {
      steps
      {
        sh 'grype dir:. --scope AllLayers'
        // grypeScan scanDest: 'dir:/tmp', repName: 'myScanResult.txt', autoInstall : 1
      }
    }
  }
}
