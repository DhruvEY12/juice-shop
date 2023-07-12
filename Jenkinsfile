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
        grypeScan scanDest: 'dir:/tmp', repName: 'myScanResult.txt'
      }
    }
  }
}
