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

           def workspaceDirs = new File(workspace).listFiles().findAll { it.isDirectory() }.collect { it.name }
            for (dir in workspaceDirs) {
            echo "Directory: ${dir}"
            }
        }
    } catch (Exception e) {
        echo "Encountered An Exception"
        currentBuild.result = "FAILURE"
        echo e.toString()
    }
} 
