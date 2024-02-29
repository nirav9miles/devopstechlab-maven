pipeline {
    agent any
    tools {
        maven 'maven3.9'
        jdk 'java17'
    }
    stages {
        stage('Git-Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/nirav9miles/devopstechlab-maven.git'
            }
        }
        
         stage('Build-maven') {
            steps {
                sh 'mvn clean package'
            }
        }   
            stage('Test-Maven') {
            steps {
                junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'
            }
        }   
            stage('Archive-Artifact') {
            steps {
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }  
               stage('Deploy-artifect') {
            steps {
               deploy adapters: [tomcat9(credentialsId: '05a472e3-3c51-48a1-aefc-34932a5cf787', path: '', url: 'http://34.125.34.209:8090/webapp')], contextPath: null, war: '**/*.war'
        }  
    }
}

}
