pipeline {
    agent any
    tools {
        maven 'mvn'
    }
    stages {
        stage('Build') {
            steps {
                sh 'rm -rf target/* && rm -rf src/build/*.jar'
                sh 'mvn clean install -DskipTests'
                sh 'ls -la target/'
                sh 'cp target/eurika-0.0.1-SNAPSHOT.jar src/build/'
            }
        }
    }
}

node {
  def commitHash = checkout(scm).GIT_COMMIT
  dir("src/build") {
    docker.withTool("docker") {
      docker.withRegistry('http://localhost:5000') {
          env.PATH = "${tool 'docker'}/bin:${env.PATH}"
          def version = "${env.BRANCH_NAME}-${new Date().format('yyyyMMdd')}-${env.BUILD_NUMBER}"
          def newApp = docker.build("eureka:${version}")
          newApp.push(version)
          sh "docker rmi eureka:${version}"
      }
    }

  }
}
