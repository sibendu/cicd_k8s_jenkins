node {

    checkout scm

    env.DOCKER_API_VERSION="1.23" 
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "hello"
    registryHost = "sibendu"
    imageName = "${registryHost}/${appName}:${tag}"
    registryUer="sibendudas"
    registryPassword="password1234"		
    env.BUILDIMG=imageName

    stage "Build"
    	sh "echo ${imageName}"
	sh "docker ps"
        sh "docker build -t ${imageName} -f applications/hello/Dockerfile applications/hello"
    
    stage "Push"
	
	sh "docker login -u ${registryUer} -p ${registryPassword}"
        sh "docker push ${imageName}"

    stage "Deploy"

        sh "sed 's#sibendu/hello:latest#'$BUILDIMG'#' applications/hello/deployment.yaml | kubectl apply -f -"
        sh "kubectl rollout status deployment/hello-kenzan"
}
