#!/usr/bin/env groovy

import java.net.URL

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
	    try{
	        withMaven(maven:'mymaven'){
	            sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
	        }
	    } finally{
	        cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
	    }
	}
	stage('package'){
	    withMaven(maven:'mymaven'){
	        sh 'mvn package'
	    }
	}
    }
