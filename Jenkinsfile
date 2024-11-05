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
                echo "Setting up environment for Windows build"
            }
        }
        stage('Build') {
            steps {
                // Run the algorithm script and output both to console and a file
                bat '''
                    @echo off
                    echo Running the algorithm script
                    ./algorithm.bat > output.txt
                    type output.txt
                '''

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
