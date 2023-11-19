pipeline {
    
    agent any
    
    tools {
        maven "mymaven"
    }
    
    stages {
        stage("Clone") {
            steps {
                git "https://github.com/Sonal0409/DevOpsCodeDemo.git"
            }
        }
        
        stage("Compile") {
            steps {
                sh "mvn compile"
            }
            
        }
        
        stage("Code Review") {
            steps {
                sh "mvn pmd:pmd"
            }
            post {
                success {
                    recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
                }
            }
        }
        
        stage("Test") {
            steps {
                sh "mvn test"
            }
            post {
                success {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage("Package") {
            steps {
                sh "mvn package"
            }
        }
    }
}