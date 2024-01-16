node
{
properties([
        pipelineTriggers([
            cron('H/5 * * * *')
        ])
    ])

def workspace="C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\clearWorkspace"
def REPO_URL="https://github.com/Ayushghagre/clearWorkspace.git"
currentBuild.result="SUCCESS"
try
{
stage("checkout")
{
   checkout scm
}
stage("clearing up Workspace")
{
def remoteBranches = bat(script: "git ls-remote --heads ${REPO_URL}", returnStdout: true).trim()
        echo remoteBranches
def branchList = remoteBranches.readLines().collect { it.split()[1].replaceAll('refs/heads/', '') }
        
   
}

}
catch(Exception e)
{
echo "Encountered  An Exception"
currentBuild.result="FAILURE"
echo e.toString()
}
}
