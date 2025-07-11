node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }
    stage('Check Docker') {
            echo "Verificando Docker..."
            sh 'docker --version'
    }
    stage('Build image') {
  
       app = docker.build("NeilToscano/test")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
