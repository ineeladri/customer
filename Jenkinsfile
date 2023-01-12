node {
      stage("Git Clone"){

        git branch: 'main', url: 'https://github.com/ineeladri/customer.git'
    }
   
    stage("Docker build"){
    sh 'docker build -t customer:latest -f Dockerfile .'
        sh 'docker image ls'
    }
withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'test', usernameVariable: 'apurva09', passwordVariable: 'password']]) {
        sh 'docker login -u apurva09 -p $password'
	}
    stage("Pushing Image to Docker Hub"){
	     sh 'docker tag customer apurva09/customer:latest'
	   sh 'docker push apurva09/customer:latest'
    }
	stage("SSH Into Server") {
def remote = [:]
remote.name = 'VMububtu18.0'
remote.host = '20.163.181.235'
remote.user = 'azureuser'
remote.password = 'Miracle@1234'
remote.allowAnyHosts = true
}
	stage("Deploy"){
sh 'docker rm -f customer||true'
sh 'docker run -p 9002:9002 -d --name customer customer:latest'
}
}
}
