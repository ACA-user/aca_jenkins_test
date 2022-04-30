node {

    checkout scm

    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {

        def customImage = docker.build("jenkinstestt/aca")

        customImage.push()
    }
}
