pipeline {
    agent any
    stages {
        stage('List Files') {
            steps {
                script {
                    def fileNames = []
                    new File('directory').eachFile {
                        if (it.isFile()) {
                            fileNames.add(it.getName())
                        }
                    }
                    properties([
                        parameters([
                            choice(name: 'FILE_NAME', choices: fileNames.join('\n'), description: 'Select a file')
                        ])
                    ])
                }
            }
        }
        // Add additional stages here as needed
    }
}
