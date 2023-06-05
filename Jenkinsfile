pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    def folderName = new Date().format("yyyy-MM-dd-HH-mm-ss")
                    git url: 'https://github.com/stackexpress-meenakshi/zip-application.git', branch: 'master', dir: folderName
                }
            }
        }

        stage('Copy and Unzip') {
            steps {
                script {
                    def folderName = new Date().format("yyyy-MM-dd-HH-mm-ss")
                    def zipFileName = "${folderName}.zip"
                    def destinationPath = "/var/www/html/${folderName}/"

                    sh "cd ${folderName} && zip -r ../${zipFileName} *"
                    sh "mkdir -p ${destinationPath}"
                    sh "cp ${zipFileName} ${destinationPath}"
                    sh "unzip ${destinationPath}${zipFileName} -d ${destinationPath}"
                    sh "rm ${destinationPath}${zipFileName}"
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    def folderName = new Date().format("yyyy-MM-dd-HH-mm-ss")
                    def sourcePath = "/var/www/html/${folderName}"
                    def destinationPath = "/var/www/html/latest"
                    def indexFilePath = "/var/www/html/index.html"

                    sh "ln -s ${sourcePath} ${destinationPath}"
                    sh "cp ${sourcePath}/index.html ${indexFilePath}"
                }
            }
        }
    }
}
