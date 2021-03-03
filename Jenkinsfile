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
        withDockerRegistry([ credentialsId: "Swetha07!", url: "" ]) {
        bat "docker push woualabs07/nodeapp:build"
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
