node
{

def branchName=env.BRANCH_NAME
def workspace="C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\"+branchName
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
def branchExists = bat(script: "git ls-remote --heads ${REPO_URL} ${branchName}", returnStdout: true).trim()
echo branchExists



}


}

catch(Exception e)
{
echo "Encountered  An Exception"
currentBuild.result="FAILURE"
echo e.toString()
}
}
