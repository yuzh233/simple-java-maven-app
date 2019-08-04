pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /Users/Harry/.m2:/root/.m2' 
            args '-v /Library/Maven/apache-maven-3.6.0/conf/settings.xml:/usr/share/maven/conf/settings.xml'
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
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

        stage('Deliver') {
            steps {
                sh 'echo "发布阶段。。。"'
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }


}

