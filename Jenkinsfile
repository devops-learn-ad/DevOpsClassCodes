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
               withMaven(maven:'admaven'){
               sh 'mvn pmd:pmd'
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
          withMaven(maven:'admaven'){
               sh 'cobertura:cobertura -Dcobertura.report.format=xml'
          }
     }     
     stage('Package'){
          withMaven(maven:'admaven'){
	    sh 'mvn package'	
	 }
     }
}
