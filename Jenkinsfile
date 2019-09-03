def GITURL = 'https://github.com/prateekdhiman27/abap_gitworkflow.git'
def BRANCH = 'master'
def PIPELINE_GITURL = 'https://github.com/prateekdhiman27/abap-ci-postman.git'
def PACKAGE = '''TESTABAPGIT'''
def COVERAGE = 80
def VARIANT = "DEFAULT"

parallel (
    "SAL":{
        node {
        	def LABEL = "SAL"
        	def HOST = "phlhdr07.phl.sap.corp"
        	def CREDENTIAL = "SAL"

        	git poll: true, branch: BRANCH, url: GITURL

        	stage('[' + LABEL + '] Preparation') {
        		deleteDir()
        		dir('sap-pipeline') {
        			bat "git clone " + PIPELINE_GITURL + " ."
        		}
        	}

        	def sap_pipeline = load "sap-pipeline/sap.groovy"
        	sap_pipeline.abap_unit(LABEL,HOST,CREDENTIAL,PACKAGE,COVERAGE)
        	sap_pipeline.abap_sci(LABEL,HOST,CREDENTIAL,PACKAGE,VARIANT)
        	sap_pipeline.sap_api_test(LABEL,HOST,CREDENTIAL)
        }
    }
