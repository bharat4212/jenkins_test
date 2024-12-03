pipeline {
    agent {
        label "linux"
    }
    
    tools {
        maven "MVN3"
    }
    
    stages {
        stage('pull scm') {
            steps {
                git credentialsId: 'github', url: 'git@github.com:bharat4212/jenkins_test.git'
            }
        }
        
        stage('build') {
            steps {
                sh "mvn -f api-gateway/ clean package"
            }
        }
        
        stage('publish') {
            agent {
                label 'windows'
            }
            steps {
                junit stdioRetention: '', testResults: 'api-gateway/target/surefire-reports/*.xml'
                archiveArtifacts 'api-gateway/target/*.jar'
            }
        }
    }
}
