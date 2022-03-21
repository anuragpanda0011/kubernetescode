node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
       app = docker.build("anurag0011/brownbagsession")
    }

    stage('Post Stage image') {
  

        app.inside {
            sh 'echo "Docker repo is reachable"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifestjob', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
