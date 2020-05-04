node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "hello"
    registryHost = "sibendu"
    imageName = "${registryHost}/${appName}:${tag}"
    registryUer="sibendudas"
    registryPassword="p@ssw0rd12"		
    env.BUILDIMG=imageName

    stage "Build"
    
        sh "docker build -t ${imageName} -f applications/hello/Dockerfile applications/hello"
    
    stage "Push"
	
	sh "docker login -u ${registryUer} -p ${registryPassword}"
        sh "docker push ${imageName}"

    stage "Deploy"

        sh "sed 's#sibendu/hello:latest#'$BUILDIMG'#' applications/hello/deployment.yaml | kubectl apply -f -"
        sh "kubectl rollout status deployment/hello-kenzan"
}
