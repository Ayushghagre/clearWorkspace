node
{

def branchName=env.BRANCH_NAME
def workspace="C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\${JOB_NAME}"+branchName
def REPO_URL="https://github.com/Ayushghagre/clearWorkspace.git"
currentBuild.result="SUCCESS"
try
{
stage("checkout")
{
   checkout scm
}
stage("clearing Workspace")
{
def branchExists = bat(script: "git ls-remote --heads ${REPO_URL} ${branchName}", returnStdout: true).trim().contains(branchName)
if(branchExists)
{
  echo "no need to clear the  workspace for the branch ${branchName}"
}
else
{
    dir(workspace)
    {
      deleteDir()
    }

}


}
}
catch(Exception e)
{
echo "Encountered  An Exception"
currentBuild.result="FAILURE"
echo e.toString()
}
}
