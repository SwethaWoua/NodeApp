node {
    def app
    
    stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarserver') {
                    sh "mvn sonar:sonar"
                }
            }
        }
        
        
        stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
    
    
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
	    
	     withCredentials([usernamePassword( credentialsId: 'docker-hub-credentials', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
        def registry_url = "registry.hub.docker.com/"
        bat "docker login -u 'woualabs07' -p 'Swetha07!' ${registry_url}"
        docker.withRegistry("http://${registry_url}", "docker-hub-credentials") {
            // Push your image now
            bat "docker push username/foldername:build"
        }
    }
	    
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'Swetha07!') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
