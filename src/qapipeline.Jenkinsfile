pipeline {
    agent any
    environment {
        QA_JOB_ENDPOINT = "http://staging-build.acko.in/job/Test_Renewal_Revamp/"
        QA_PINCODE_ENDPOINT = "http://staging-build.acko.in/job/Master_Service_Pincode_Test/"
        MASTER_SERVICE_RENEWAL_TEST = "http://staging-build.acko.in/job/Master_Service_Renewal_Test/"
        MASTER_SERVICE_VARIANT_TEST = "http://staging-build.acko.in/job/Master_Service_Variant_Test/"
        RULE_ENGINE_ROI_NEWCAR = "http://172.31.42.16:8080/view/Pricing/job/ruleEngine_ROI_NewCar_GoodAndBadRoi/"
        AUTO_PRICING = "http://172.31.42.16:8080/view/Pricing/job/Auto-Pricing/"
        OLA_ELECTRIC = "http://172.31.42.16:8080/view/Pricing/job/olaElectric_Find_Failed_Pincodes/"
        JENKINS_DEV_TOKEN = "MTFiMWY5YzFlOWRmNWZiMGU2MmIyMjg3ZTZjNjViMjgwMg=="
        BUILDSTATUS = "FAILURE"
    }
    stages {
        stage ('Run test') {
            parallel {
                stage("ruleEngine_ROI_NewCar_GoodAndBadRoi") {
                    agent {
                        label 'master'
                    }
                    steps{
                        echo "Steps"
                        script {
                            def handle = triggerRemoteJob job: "${RULE_ENGINE_ROI_NEWCAR}", auth: CredentialsAuth(credentials: 'JENKINS_QA_API_TOKEN'), shouldNotFailBuild: true
                            BUILDSTATUS = handle.getBuildResult().toString()
                            echo BUILDSTATUS;
                            if (BUILDSTATUS == "FAILURE") {
                               error('Test job failure')
                            }
                        }
                    }
                }
                stage("Auto-Pricing") {
                    agent {
                        label 'master'
                    }
                    steps{
                        echo "Steps"
                        script {
                            def handle = triggerRemoteJob job: "${AUTO_PRICING}", auth: CredentialsAuth(credentials: 'JENKINS_QA_API_TOKEN'), shouldNotFailBuild: true
                            BUILDSTATUS = handle.getBuildResult().toString()
                            echo BUILDSTATUS;
                            if (BUILDSTATUS == "FAILURE") {
                               error('Test job failure')
                            }
                        }
                    }
                }
                stage("olaElectric_Find_Failed_Pincodes") {
                    agent {
                        label 'master'
                    }
                    steps{
                        echo "Steps"
                        script {
                            def handle = triggerRemoteJob job: "${OLA_ELECTRIC}", auth: CredentialsAuth(credentials: 'JENKINS_QA_API_TOKEN'), shouldNotFailBuild: true
                            BUILDSTATUS = handle.getBuildResult().toString()
                            echo BUILDSTATUS;
                            if (BUILDSTATUS == "FAILURE") {
                               error('Test job failure')
                            }
                        }
                    }
                }
            }

        }
    }
}

// curl --silent -X POST http://staging-build.acko.in/job/Test_Renewal_Revamp/=uat --header 'Authorization: Basic MTFiMWY5YzFlOWRmNWZiMGU2MmIyMjg3ZTZjNjViMjgwMg=='