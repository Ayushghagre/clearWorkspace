node {
    properties([
        pipelineTriggers([
            cron('H/5 * * * *')
        ])
    ])

    def workspace = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\clearWorkspace"
    def REPO_URL = "https://github.com/Ayushghagre/clearWorkspace.git"
    currentBuild.result = "SUCCESS"

    try {
        stage("checkout") {
            checkout scm
        }

        stage("clearing up Workspace") {
            def remoteBranches = bat(script: "git ls-remote --heads ${REPO_URL}", returnStdout: true).trim()
            

           

def branchList = remoteBranches.readLines()
                   .findAll { it.contains('refs/heads/') } // Filter lines containing 'refs/heads/'
                   .collect { it.split()[1].replaceAll('refs/heads/', '') } // Extract branch names

def workspaceDirs = bat(script: "dir /B /A:D ${workspace}", returnStdout: true).trim().split("\\r?\\n")

        // Deleting directories that don't have a corresponding remote branch
        workspaceDirs.each { dir ->
            if (!branchList.contains(dir)) {
                echo "Deleting workspace for branch: ${dir}"
                bat "rmdir /S /Q ${workspaceRootDir}\\${dir}"
            }
        }

        }
    } catch (Exception e) {
        echo "Encountered An Exception"
        currentBuild.result = "FAILURE"
        echo e.toString()
    }
}
