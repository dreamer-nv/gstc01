#!/usr/bin/env groovy
@Library('ares-lib') _

def dev = [ 
	"hostname": "3.232.239.122",
	"port": "50001",
	"external_alias": "build",
	"transport": "",
	"package": "",
	"software_component": "",
	"tfc_id": "",
	"build_phase": "",
	"credentials": "gCTS_source",
	"pipelinename": "",
  	"repo_id": "i079666gcts1",
  	"commit_id": "",
	"aunitresultKey": "AUNIT_FOR_TCK",
	"atcresultKey": "ATC_FOR_TCK"
]

def integrate = [ 
	"hostname": "34.228.253.201",
	"port": "50000",
	"external_alias": "build",
	"transport": "",
	"package": "",
	"software_component": "",
	"tfc_id": "",
	"build_phase" : "",
	"credentials": "gCTS_target",
	"pipelinename": "",
  	"repo_id": "i079666gcts1",
  	"commit_id": "",
	"aunitresultKey": "AUNIT_FOR_TCK",
	"atcresultKey": "ATC_FOR_TCK"
]



pipeline {
  agent any
  stages {
    stage('data declaration') {
      steps {
        script {
          dev.pipelinename = "${env.JOB_BASE_NAME}_${env.BUILD_NUMBER}"
          integrate.pipelinename = "${env.JOB_BASE_NAME}_${env.BUILD_NUMBER}"
          echoParameters(dev) 
          echoParameters(integrate)
          } //script
        } // steps
      } // stage
    stage('integrate') {
      steps {
        script {
          integrate.commit_id = sh(returnStdout: true, script: 'git rev-parse HEAD')
          echo 'integrate.commit_id is :'+integrate.commit_id 
          integrate.transport = pullByCommitgCTSHTTP(integrate)                  
          } //script
        } // steps
      } // stage
    } //stages
  } //pipeline
