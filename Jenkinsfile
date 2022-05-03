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
            agent {
                docker {
                    image "jenkinstestt/aca:${env.BUILD_NUMBER}"
                    reuseNode true
                }
            }
        }

}
