pipeline {
    agent any
    tools {
        maven 'mvn'
    }
    stages {
        stage('Build') {
            steps {
                sh 'rm -rf target/* && rm -rf src/build/*.jar'
                sh 'docker run -it --rm --name my-maven-project -v "$(pwd)":/usr/src/mymaven -w /usr/src/mymaven maven:3.3-jdk-8 mvn clean install -DskipTests'
                sh 'ls -la target/'
                sh 'cp target/eurika-0.0.1-SNAPSHOT.jar src/build/'
            }
        }
    }
}