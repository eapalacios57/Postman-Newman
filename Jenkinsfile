pipeline {
    agent {
        label 'nodo-vm' 
    }
  stages {
    stage('run collection') {
      steps {
        git branch: '${BRANCH_NAME}', credentialsId: '995d58f6-eb07-41cc-ab62-4160537621a9', url: 'https://github.com/eapalacios57/Postman-Newman.git'
        // sh 'docker run --rm -v ${PWD}:/etc/newman -w /etc/newman -t postman/newman run Collection.postman_collection.json -e enviroment.json --color off --disable-unicode'
        sh 'docker ps'
      }
    }
  }
}
// node {
//     try {
//         notifyBuild('STARTED')

//         stage('Prepare code') {
//             echo 'do checkout stuff'
//         }

//         stage('Testing') {
//             sleep 200
//             echo 'Testing'
//             echo 'Testing - publish coverage results'
//         }

//         stage('Staging') {
//             echo 'Deploy Stage'
//         }

//         stage('Deploy') {
//             echo 'Deploy - Backend'
//             echo 'Deploy - Frontend'
//         }

//   } catch (e) {
//     // If there was an exception thrown, the build failed
//     currentBuild.result = "FAILED"
//     throw e
//   } finally {
//     // Success or failure, always send notifications
//     notifyBuild(currentBuild.result)
//   }
// }
// def notifyBuild(String buildStatus = 'STARTED') {
//   // build status of null means successful
//   buildStatus =  buildStatus ?: 'SUCCESSFUL'

//   // Default values
//   def colorName = 'RED'
//   def colorCode = '#FF0000'
//   def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
//   def summary = "${subject} (${env.BUILD_URL})"

//   // Override default values based on build status
//   if (buildStatus == 'STARTED') {
//     color = 'YELLOW'
//     colorCode = '#FFFF00'
//   } else if (buildStatus == 'SUCCESSFUL') {
//     color = 'GREEN'
//     colorCode = '#00FF00'
//   } else {
//     color = 'RED'
//     colorCode = '#FF0000'
//   }

//   // Send notifications
//   slackSend (color: colorCode, message: summary)
// }


