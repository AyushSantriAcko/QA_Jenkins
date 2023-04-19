pipeline {
 agent any
    stages {
            stage('Run Tests') {
                parallel {
                   stage('Master_Service_Pincode_Test') {
                       steps{
                        build job: 'Master_Service_Pincode_Test'
                       }
                    }
                   stage("Renewal Revamp") {
                       steps{
                           build job: "Test_Renewal_Revamp"
                       }
                   }
                 }
            }
    }
}