#!groovy

import groovy.json.JsonSlurperClassic

node {

    def HUB_ORG_DH=env.HUB_ORG_DH
    def SFDC_HOST_DH=env.SFDC_HOST_DH
    def CONNECTED_APP_CONSUMER_KEY_DH=env.CONNECTED_APP_CONSUMER_KEY_DH
    def JWT_CRED_ID_DH=env.JWT_CRED_ID_DH
    def TEST_LEVEL='RunLocalTests'
    def PACKAGE_NAME='0Ho1U000000CaUzSAK'
    def PACKAGE_VERSION
    def SF_INSTANCE_URL = env.SF_INSTANCE_URL ?: "https://login.salesforce.com"

   //  def toolbelt = tool 'toolbelt'
    echo("HUB_ORG_DH "+${HUB_ORG_DH})


    // -------------------------------------------------------------------------
    // Check out code from source control.
    // -------------------------------------------------------------------------

    stage('checkout source') {
        checkout scm
    }


    // -------------------------------------------------------------------------
    // Run all the enclosed stages with access to the Salesforce
    // JWT key credentials.
    // -------------------------------------------------------------------------
    
    withEnv(["HOME=${env.WORKSPACE}"]) {
        
        withCredentials([file(credentialsId: JWT_CRED_ID_DH, variable: 'server_key_file')]) {

            // -------------------------------------------------------------------------
            // Authorize the Dev Hub org with JWT key and give it an alias.
            // -------------------------------------------------------------------------

            stage('Authorize DevHub') {
               // rc = command "${toolbelt}/sfdx auth:jwt:grant --instanceurl ${SFDC_HOST_DH} --clientid ${CONNECTED_APP_CONSUMER_KEY_DH} --username ${HUB_ORG_DH} --jwtkeyfile ${JWT_CRED_ID_DH} --setdefaultdevhubusername --setalias HubOrg"
                // if (rc != 0) {
                    // error 'Salesforce dev hub org authorization failed.'
                // }
            }
        }
    }
}

def command(script) {
    if (isUnix()) {
        return sh(returnStatus: true, script: script);
    } else {
        return bat(returnStatus: true, script: script);
    }
}
