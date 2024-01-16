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
        stage("checkout") {
            checkout scm
        }

        stage("clearing up Workspace") {
            def remoteBranches = bat(script: "git ls-remote --heads ${REPO_URL}", returnStdout: true).trim()
            

           

def branchList = remoteBranches.readLines()
                   .findAll { it.contains('refs/heads/') } // Filter lines containing 'refs/heads/'
                   .collect { it.split()[1].replaceAll('refs/heads/', '') } // Extract branch names

def workspaceDirs = bat(script: "dir /B /A:D ${workspace}", returnStdout: true).trim().split("\\r?\\n")

        workspaceDirs.each { dir ->
            if (!branchList.contains(dir)) {
                echo "Deleting workspace for branch: ${dir}"
                bat "rmdir /S /Q ${workspace}\\${dir}"
            }
        
        }
    } catch (Exception e) {
        echo "Encountered An Exception"
        currentBuild.result = "FAILURE"
        echo e.toString()
    }
}
