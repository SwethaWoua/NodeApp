node {
    def app
	
environment {
    registry = "woualabs07/nodeapp"
    registryCredential = 'Santhiya'
    //dockerImage = ''
  }
    
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
	    
	    docker.withRegistry( '', registryCredential ) {
                          app.push()
		    app.push("${env.BUILD_NUMBER}")
                 app.push("latest")
            } 
	  /* 
	You would need to first register with DockerHub before you can push images to your account
		*/
       /* docker.withRegistry('https://registry.hub.docker.com', 'Santhiya') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            }*/ 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
