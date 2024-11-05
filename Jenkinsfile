pipeline {
    agent any
    options {
        buildDiscarder(logRotator(daysToKeepStr: '10', numToKeepStr: '10'))
        timeout(time: 12, unit: 'HOURS')
        timestamps()
    }
    stages {
        stage('Requirements') {
            steps {
                // No need for chmod on Windows, so this step is removed.
                echo "Setting up environment for Windows build"
            }
        }
        stage('Build') {
            steps {
                // Use bat to execute a Windows batch script
                bat('./algorithm.bat')

                // Archive the report
                archiveArtifacts(
                    allowEmptyArchive: true,
                    artifacts: '*.txt',
                    fingerprint: true,
                    onlyIfSuccessful: true
                )
            }
        }
    }
}
