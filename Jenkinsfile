pipeline  {
  agent any
  environment {
	dockerRegistry="dagoncant/ejereoi"
	dockerCredentials="dockerhub"
	projectVersion="1.0"
	gitRepository="https://github.com/dagoncant/CursoEOI.git"
  }
stages {
  stage('limpiar') {
	steps {
		cleanWs()
	}
  }
  stage('checkout') {
	steps{
		script {
			git branch: 'main',
			url: gitRepository
		}
	}
  }
  stage('buildear') {
	steps {
		script {
			dockerImage=docker.build dockerRegistry
		}
	}
  }
  stage('test') {
	steps {
			sh 'docker run $dockerRegistry'

	}
  }
  stage('desplegar') {
	steps {
		script {
		    docker.withRegistry('',dockerCredentials) {
			    dockerImage.push()
		    }
		}
	}
  }
}

  post{
	failure {
     	echo 'Error:El pipeline ha fallado'
    }
  }
}
