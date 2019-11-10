#!/usr/bin/env groovy

node{
    stage('Git checkout'){
        git 'https://github.com/Rajesh-Mushtigunta/DevOpsClassCodes.git'
    }
    stage('compile'){
        withMaven(maven:'mymaven'){
            sh 'mvn compile'
        }
    }
    stage('review'){
        withMaven(maven:'mymaven'){
            sh 'mvn pmd:pmd'
        }
    }
    stage('Test'){
        try{
            withMaven(maven:'mymaven'){
                sh 'mvn test'
            } 
        } finally{
            junit 'target/surefire-reports/*.xml'
        }
    }
	stage('code Coverage check'){
		withMaven(maven:'mymaven'){
		sh 'mvn cobertura:cobertura'
		}
	}	
    }
