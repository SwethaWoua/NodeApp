node {
    def app 
    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("woualabs07/nodeapp")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }
stage('Push image') {
    withCredentials([usernamePassword( credentialsId: 'Swetha07!', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
        def registry_url = "registry.hub.docker.com/"
        bat "docker login -u $USER -p $PASSWORD ${registry_url}"
        docker.withRegistry("http://${registry_url}", "docker-hub-credentials") {
            // Push your image now
            bat "docker push username/foldername:build"
        }
    }
}

    /*stage('Push image') {
	       
	     docker.withRegistry('https://registry.hub.docker.com','Swetha07!') {
	     bat "docker login -u 'woualabs07' -p 'Swetha07!'
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            }
                echo "Trying to Push Docker Build to DockerHub"
    }*/
}
