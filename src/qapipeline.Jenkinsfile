pipeline {
echo"Start of pipeline......."
 agent any
    stages {
    echo "Under Stages....."
            stage('Run Tests') {
            echo "Under Stage....."
                parallel {
                echo "Under parallel....."
                   stage('Master_Service_Pincode_Test') {
                       steps{
                       echo "Under pincode....."
//                         build job: 'Master_Service_Pincode_Test'
                       }
                    }
                   stage("Renewal Revamp") {
                       steps{
                       echo "Under revamp....."
//                            build job: "Test_Renewal_Revamp"
                       }
                   }
                 }
            }
    }
}