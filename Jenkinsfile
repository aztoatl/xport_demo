node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }
 stages {
    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("aztoatl/web_server:test")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }
  
    stage('Push image') 
	when { branch 'master' }
	steps{
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
    stage('merge to master') 
	when { branch 'test'}
	steps{
	
	sh 'git merge master'
	
	}
    
 }
}
