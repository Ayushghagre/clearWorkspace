node {
    properties([
        pipelineTriggers([
            cron('H/5 * * * *')
        ])
    ])

    def workspace = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\"
    def REPO_URL = "https://github.com/Ayushghagre/clearWorkspace.git"
    currentBuild.result = "SUCCESS"

    try {
        

        stage("clearing up Workspace") {
            def remoteBranches = bat(script: "git ls-remote --heads ${REPO_URL}", returnStdout: true).trim()

            def branchList = remoteBranches.readLines()
                   .findAll { it.contains('refs/heads/') } 
                   .collect { it.split()[1].replaceAll('refs/heads/', '') } 

            def workspaceDirs = bat(script: "dir /B  ${workspace}", returnStdout: true).trim().split("\\r?\\n")
            for (dir in workspaceDirs) {
            echo "Directory: ${dir}"
               }
            for (dir in workspaceDirs) {
    if (!branchList.contains(dir)) {
        echo "Deleting workspace for branch: ${dir}"
        bat "rmdir /S /Q \"${workspace}${dir}\""


    }
}
        }
    } catch (Exception e) {
        echo "Encountered An Exception"
        currentBuild.result = "FAILURE"
        echo e.toString()
    }
} 
