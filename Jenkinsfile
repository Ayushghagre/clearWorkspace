node
{
def branchName=env.BRANCH_NAME
def workspace="C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\clear_workspace_"+branchName
currentBuild.result = 'SUCCESS'
try{
stage("checkout")
{
    checkout scm
}
stage("clearing Workspace")
{
   def branchesToExclude = ["main","feature1","feature2","feature3"]
   if(branchesToExclude.contains(branchName))
   {
    echo "no need to delete the workspace for the branch ${branchName}"

   }
   else
   {
    dir(workspace)
    {
      deleteDir();
    }

   }

}
}
catch(Exception e)
{
  currentBuild.result="FAILURE"
  echo "encountered an Exception"
  echo  e.toString();
}
}
