pipeline {
    agent any

    tools {
        maven 'mymaven'
    }
    
    stages {
        stage('Compile') {
            steps {
                echo 'Compiling'
                sh 'mvn compile'
            }
        }
        stage('Code Review') {
            steps {
                echo 'code review'
                sh 'mvn pmd:pmd'
            }
        }
        stage('Unit Test') {
            steps {
                echo 'unit testing'
                sh 'mvn test'
            }
        }
        stage('Coverage') {
            steps {
                echo 'coverage analysis'
                sh 'mvn verify'
            }
        }
        stage('Package') {
            agent { label 'linux_jenkins_slave1' }
            steps {
                echo 'packaging'
                sh 'mvn package'
            }
        }
        stage('Publish') {
            steps {
                echo 'publishing to jfrog'
                sh 'mvn -U deploy -s settings.xml'
            }
        }
    }
}
