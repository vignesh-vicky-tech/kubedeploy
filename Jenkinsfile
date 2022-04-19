node {
    def app

    stage('Clone repository') {
      

        checkout scm
        echo "hello"
    }
    
    stage('Clone') {
      

        
        echo "good morning"
    }

    stage('Build image') {
  
       app = docker.build("vigneshvicky12345/demo")
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatejob"
                build job: 'update', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
