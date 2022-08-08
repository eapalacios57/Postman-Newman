def branchEnv = ''
pipeline {
    agent {
        label 'master' 
    }
    // triggers{
    //     cron(env.BRANCH_NAME.equals("stage") ? '40 14 * * 1' : env.BRANCH_NAME.equals("master") ? '00 14 * * 1': '')
    // }
  stages {
    stage('Pruebas'){
      when { anyOf { branch 'master';} }
      steps{
        sh 'pwd'
        sh 'uname -a'
        sh 'ls -la'
        stash includes: "Jenkinsfile.weblogic", name: 'files'
      }
    }
    // stage ('S3 upload Artefactory') {
    //     when { anyOf { branch 'develop'; tag "v*-release"; tag "v*"} } 
    //     steps {
    //         script {
    //         branchEnv = BRANCH_NAME
    //            if(BRANCH_NAME ==~ /^v\d*\.\d*\.\d*\.\d*-release$/){
    //                 branchEnv = 'stage'
    //            }
    //            if(BRANCH_NAME ==~ /^v\d*\.\d*\.\d*\.\d*/){
    //                 branchEnv = 'master'
    //            }    
    //         }
    //             sh 'ls -la'
    //             sh 'pwd'
    //             sh 'echo ${branchEnv}'
    //             withAWS(region:'us-east-1', credentials:'e07e68a1-4303-4114-9fd2-1fe23fedfea2'){
    //               //Opcion Uno
    //               aws s3 cp jenkinsfile s3://testbucketsimon-jenkins/simon/
    //               //Opcion Dos
    //               s3Upload(file:"Jenkinsfile.bk", bucket:"testbucketsimon-jenkins", path:"simon/", pathStyleAccessEnabled: true,)
    //       }
    //     }

    // }
 stage('Smoke Test') {
   steps {
       sh 'hostname'
       unstash 'files'
        }
    post{
        always{
            sh 'hostname'
            node('Linux'){
                script{
                  if(BRANCH_NAME == 'master'){
                    sh 'docker ps'
                    unstash 'files'
                    sh 'mv Jenkinsfile.weblogic JenkinsTest'
                    sh 'ls -la'
                  }
                }
            }
        }
      }
    }
  }
}

