node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("jenkinstestt/aca")
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
    stage('Docker run') {
        // docker.image("jenkinstestt/aca:${env.BUILD_NUMBER}")
        sh("docker run -tid -p 8081:80 jenkinstestt/aca:${env.BUILD_NUMBER}")
    }

}
