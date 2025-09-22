pipeline {

    agent any
    stages {
	
        stage('CLONE SCM') {
            steps {
                echo 'This stage clones SC from GIT repo'				
				git branch: 'main', url: 'https://github.com/Sk-Nagul-09/mindcircuit16d.git'
            }
        }
        
        stage('Build upto compile') {
            steps {
                echo 'This stage builds the package code using maven'
				sh 'mvn clean compile'
            }
        }
        
        stage('Build upto package') {
            steps {
                echo 'This stage builds the package code using maven'
				sh 'mvn clean package'
            }
        }
        
        stage('Build upto verify') {
            steps {
                echo 'This stage builds the package code using maven'
				sh 'mvn clean verify'
            }
        }
		
        stage('Build Artifact') {
            steps {
                echo 'This stage builds the code using maven'
				sh 'mvn clean install'
            }
        }
		
        stage('Deploy to Tomcat') {
            steps {
                echo 'This stage deploys .war to tomcat webserver'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://54.242.51.179:8080/')], contextPath: 'Nagull', war: '**/*.war'
            }
        }	
        
        stage('Deploy to Multiple Environments') {
            parallel {
                stage('Lab') {
                    steps {
                        echo 'DEPLOYING ON LAB...'
                       // deploying on LAB TOMCAT WEB SERVER 
                   }
                }
                stage('sbox') {
                    steps {
                        echo 'DEPLOYING ON sbox...'
                       // deploying on SBOX  TOMCAT WEB SERVER 
                   }
                    }
                
                stage('UAT') {
                    steps {
                        echo 'DEPLOYING ON UAT...'
                      // deploying on UAT  TOMCAT WEB SERVER 
                   }
                }
            }
        }
    }
}
