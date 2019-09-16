node('docker') {
    def app
 
    stage('Clone repository') {
        checkout scm
    }
 
    stage('Build image') {
        imageName="ucsdets/bipn145_wi19"
        subdir="BIPN145_WI19"
        sh("docker build -t ${imageName} ${subdir}/")
        app = docker.image(imageName)
    }
 
    stage('Push image') {
        shortCommit = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${shortCommit}")
            app.push("latest")
        }
    }
}
