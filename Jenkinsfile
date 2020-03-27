#!/usr/bin/env groovy
import hudson.model.*
import java.net.URL

node{
     stage('GIT Checkout'){
	git 'https://github.com/devops-learn-ad/DevOpsClassCodes.git'
     }
     stage('Compile the Code'){
	    withMaven(maven:'admaven'){
	    sh 'mvn compile'
	}
     }
     stage('ReviewofCode'){
          try {
               withMaven(maven:'admaven'){
               sh 'mvn pmd:pmd'
               }
               }finally{
                    pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
               }     
               }
     stage('Test the Code'){
          try {
               withMaven(maven:'admaven'){
                    sh 'mvn test'
                    }
                    }finally{
                         junit 'target/surefire-reports/*.xml'
                    }
               
          }
     stage('Code Coverage Check'){
          try{
              withMaven(maven:'admaven'){
               sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
          }
          }finally{
               cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
          }
     }  
     stage('Package'){
          withMaven(maven:'admaven'){
	    sh 'mvn package'	
	 }
     }
}
