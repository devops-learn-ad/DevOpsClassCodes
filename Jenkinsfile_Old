#!/usr/bin/env groovy
import hudson.modle.*
import java.net.URL

node{
    stage('Git Checkout'){
	git 'https://github.com/devops-learn-ad/DevOpsClassCodes.git'
    }
    stage('Compile'){
        withMaven(maven: 'mymaven'){
        sh 'mvn compile'
	}
    }
    stage('Test'){
      try {
        withMaven(maven: 'mymaven'){
         sh 'mvn test'
	   }
	} finally{
	  junit 'target/surefire-reports/*.xml'
	}
    }
    stage('Package'){
        withMaven(maven: 'mymaven'){
        sh 'mvn package'
	}
    }
}
