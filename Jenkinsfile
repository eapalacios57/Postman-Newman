def branchEnv = ''
pipeline {
    agent {
        label 'nodo-vm' 
    }
    triggers{
        cron(env.BRANCH_NAME.equals("stage") ? '40 14 * * 1' : env.BRANCH_NAME.equals("master") ? '00 14 * * 1': '')
    }
  stages {
    stage ('SonarQube analysis') {
      when { anyOf { branch 'develop'; tag "v*-release"; tag "v*" } }
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
      sh 'echo $branchEnv'
    }
    }
    stage('Smoke Test') {
      when { anyOf {  branch 'develop'; tag "v*-release"; tag "v*" } }
      steps {
        git branch: '${branchEnv}', credentialsId: '995d58f6-eb07-41cc-ab62-4160537621a9', url: 'https://github.com/eapalacios57/Postman-Newman.git'
        // sh 'docker run --rm -v ${PWD}:/etc/newman -w /etc/newman -t postman/newman run Collection.postman_collection.json -e enviroment.json --color off --disable-unicode'
        sh 'docker ps'
      }
    }
  }
}

