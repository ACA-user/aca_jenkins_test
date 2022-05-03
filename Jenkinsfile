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
        sh '''
              #!/bin/bash
              result=`docker ps |grep -wc 'jenkinstest'`
              echo ${result}
              if (( ${result}>0 )); then
                docker rm -f jenkinstest
              fi
              docker run -tid -p 8081:80 --name jenkinstest jenkinstestt/aca:${env.BUILD_NUMBER}
        '''
    }
}
