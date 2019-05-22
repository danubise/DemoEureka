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