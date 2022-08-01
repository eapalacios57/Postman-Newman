pipeline {
    agent {
        label 'nodo-vm' 
    }
    triggers{
        cron(env.BRANCH_NAME.equals("stage") ? '15 11 * * 1' : env.BRANCH_NAME.equals("master") ? '20 11 * * 1': '')
    }
  stages {
    stage('Smoke Test') {
      when { anyOf { branch 'stage'; branch 'master' } }
      steps {
        git branch: '${BRANCH_NAME}', credentialsId: '995d58f6-eb07-41cc-ab62-4160537621a9', url: 'https://github.com/eapalacios57/Postman-Newman.git'
        // sh 'docker run --rm -v ${PWD}:/etc/newman -w /etc/newman -t postman/newman run Collection.postman_collection.json -e enviroment.json --color off --disable-unicode'
        sh 'docker ps'
      }
    }
  }
}