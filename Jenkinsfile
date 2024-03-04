def pipelineContext = [:]
node {
    def registryProjet='registry.gitlab.com/dounmogni-nicolas/jenkins' //nom du registry(compte gitlab + nom_du_repository)
    def IMAGE="${registryProjet}:version-${env.BUILD_ID}"  //image est egale a nom du registry:tag 
    
    stage ('Clone') {
        
        git 'https://github.com/dounmogni/jbuild.git'
    }
    def img = stage ('Build') {
        
        docker.build("$IMAGE", '.')
    }
   
    stage('Run') {
					img.withRun("--name run-$BUILD_ID -p 80:80") { c ->
						sh 'curl localhost'
          }					
		}
     stage ('Push') {
         docker.withRegistry('https://registry.gitlab.com', 'reg1') {
             img.push 'latest'
             img.push()
             
         } 
     }
}

