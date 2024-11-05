pipeline {
    agent any
    
    tools {
        maven 'MAVEN3'
        jdk 'JAVA17'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/keertikrith/CI-CD.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat_credentials', 
                                       path: '', 
                                       url: 'http://15.207.88.81:8080')], 
                       contextPath: '/my-maven-webapp', 
                       war: 'target/*.war'
            }
        }
    }
    
    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
