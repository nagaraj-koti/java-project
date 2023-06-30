pipeline {
    agent any
tools{
    maven "MAVEN_3.9"
}
    stages {
        stage('Clone') {
            steps {
                // git branch:'prod', url: 'ttps://github.com/nagaraj-koti/java-project.git'
                git branch:"main", url: 'https://github.com/nagaraj-koti/java-project.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Deploy'){
            steps{
            deploy adapters: [tomcat9(url: 'http://3.108.217.75:8080/', 
                              credentialsId: 'tomcat-server-cred')], 
                     war: 'target/*.war',
                     contextPath: 'hello-app'
            }
        }

    }
    post{
        always{
            mail bcc: '', body: '''$BUILD_NUMBER $BUILD_NAME

jenkins $BUILD_URL''', cc: '', from: '', replyTo: '', subject: 'jenkins job', to: 'rayhubli@gmail.com'
        }
    }
}
