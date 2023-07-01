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
            deploy adapters: [tomcat9(url: 'http://13.233.151.223:8080/', 
                              credentialsId: 'tomcat-server-cred')], 
                     war: 'target/*.war',
                     contextPath: 'hello-app'
            }
        }

    }
    post{
        always{
            mail bcc: '', body: "${env.BUILD_NUMBER} - ${env.BUILD_NAME} jenkins ${env.BUILD_URL}", cc: '', from: '', replyTo: '', subject: 'jenkins job', to: 'rayhubli@gmail.com'
        }
    }
}
