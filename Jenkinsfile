pipeline {
    agent none
    tools{
        maven 'mymaven'
    }
    stages {
        stage('Compile') {
            agent any
            steps {
                echo 'Compiling'
                sh 'mvn compile'
            }
        }
        stage('Code Review') {
            agent any
            steps {
                echo 'code review'
                sh 'mvn pmd:pmd'
            }
        }
        stage('Unit Test') {
            agent any
            steps {
                echo 'unit testing'
                sh 'mvn test'
            }
        }
        stage('Coverage') {
            agent any
            steps {
                echo 'coverage analysis'
                sh 'mvn verify'
            }
        }
        stage('Package') {
            agent label {'linux_jenkins_slave1'}
            steps {
                echo 'package analysis'
                sh 'mvn package'
            }
        }
        stage('Publish') {
            agent any
            steps {
                echo 'publishing to jfrog'
                sh 'mvn -U deploy -s settings.xml'
            }
        }
    }
}

