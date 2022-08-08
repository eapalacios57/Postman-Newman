def branchEnv = ''
pipeline {
    agent {
        label 'nodo-vm' 
    }
    // triggers{
    //     cron(env.BRANCH_NAME.equals("stage") ? '40 14 * * 1' : env.BRANCH_NAME.equals("master") ? '00 14 * * 1': '')
    // }
  stages {
    stage('Pruebas Sleep'){
      when { expression { BRANCH_NAME  ==~ /^v\d*\.\d*\.\d*\.\d*/ } } 
      steps{
          script{
              sleep(time:1,unit:"MINUTES")
          }
      }
    }
    stage ('S3 upload Artefactory') {
        when { anyOf { branch 'develop'; tag "v*-release"; tag "v*"} } 
        steps {
            script {
            branchEnv = BRANCH_NAME
               if(BRANCH_NAME ==~ /^v\d*\.\d*\.\d*\.\d*-release$/){
                    branchEnv = 'stage'
               }
               if(BRANCH_NAME ==~ /^v\d*\.\d*\.\d*\.\d*/){
                    branchEnv = 'master'
               }    
            }
                sh 'ls -la'
                sh 'pwd'
                sh 'echo ${branchEnv}'
                withAWS(region:'us-east-1', credentials:'e07e68a1-4303-4114-9fd2-1fe23fedfea2'){
                  s3Upload(file:"Jenkinsfile.bk", bucket:"testbucketsimon-jenkins", path:"simon/", pathStyleAccessEnabled: true,)
          }
        }

    }
    stage('Smoke Test') {
      when { anyOf {  branch 'develop'; tag "v*-release"; tag "v*" } }
      steps {
        git branch: '${branchEnv}', credentialsId: '995d58f6-eb07-41cc-ab62-4160537621a9', url: 'https://github.com/segurosbolivar/tests-on-enviroments/'
        // sh 'docker run --rm -v ${PWD}:/etc/newman -w /etc/newman -t postman/newman run Collection.postman_collection.json -e enviroment.json --color off --disable-unicode'
        sh 'docker ps'
      }
    }
  }
}

