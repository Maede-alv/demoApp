pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Maede-alv/demoApp.git', branch: 'master'
            }
        }
        
        stage('Show Versions') {
            steps {
                sh '''
                    echo "Java version:"
                    java -version
                    echo "Maven version:"
                    mvn --version
                    echo "Current directory:"
                    pwd
                    ls -la
                '''
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
        
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                echo '📦 Artifact archived successfully!'
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}