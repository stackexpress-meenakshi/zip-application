pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    def timeStamp = new Date().format("yyyy-MM-dd-HH-mm-ss")
                    def folderName = timeStamp
                    def zipFileName = "${folderName}.zip"
                    def destinationPath = "/var/www/html/${folderName}/"
                    def sourcePath = "/var/www/html/${folderName}"
                    def destinationPathLatest = "/var/www/html/latest"
                    def indexFilePath = "/var/www/html/index.html"

                    sh "git clone https://github.com/stackexpress-meenakshi/zip-application.git ${folderName}"
                    
                    sh "cd ${folderName} && zip -r ../${zipFileName} *"
                    sh "mkdir -p ${destinationPath}"
                    sh "cp ${zipFileName} ${destinationPath}"
                    dir(destinationPath) {
                        sh "unzip ${zipFileName}"
                        sh "rm ${zipFileName}"
                    }
                    
                    sh "ln -s ${sourcePath} ${destinationPathLatest}"
                    sh "rm ${indexFilePath}" // Remove existing index.html if present
                    sh "cp ${sourcePath}/index.html ${indexFilePath}" // Copy the repository's index.html to /var/www/html/
                }
            }
        }
    }
}
