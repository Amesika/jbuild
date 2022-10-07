def pipelineContext = [:]
node {

   def registryProjet='registry.hub.docker.com/amesika/home'
	 def IMAGE="${registryProjet}:version-${env.BUILD_ID}"

	 echo "IMAGE = $IMAGE"

    stage('Clone') {
    			checkout scm
		}

		def img = stage('Build') {
					docker.build("$IMAGE",  '.')
		}
	
		stage('Run') {
					img.withRun("--name run-$BUILD_ID -p 80:80") { c ->
						sh 'curl localhost'
          }					
		}

		stage('Push') {
					docker.withRegistry("https://registry.hub.docker.com", 'DockerHub') {
							img.push 'latest'
              img.push()
					}
		}
 
}

