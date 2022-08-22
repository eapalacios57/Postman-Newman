pipeline {
   agent any
    environment {
      WEBLOGIC_CREDENTIAL = credentials('6277405c-0a82-4023-bcfe-0b545ba9bccb')
    }
   stages {
      stage('Generate File') {
         steps {
          echo '¡¡¡#Hello World!!!'
          //  script {
          //   wrap([$class: 'MaskPasswordsBuildWrapper', varPasswordPairs: [[password: WEBLOGIC_CREDENTIAL_PSW]]]) {
          //     withEnv (["WEBLOGIC_CREDENTIAL_PSW=${WEBLOGIC_CREDENTIAL_PSW}"]){
          //   //  wrap([$class: 'MaskPasswordsBuildWrapper', varPasswordPairs: [[password: '$WEBLOGIC_CREDENTIAL_PSW']]]) {
          //    def remote = [:]
          //    remote.name = 'test'
          //    remote.host = '192.168.100.158'
          //    remote.user = 'birc'
          //    remote.port = 22
          //    remote.password = 's1st3m4s'
          //    remote.allowAnyHosts = true
          //    sshCommand remote: remote, command: 'docker ps '
          //   //  logFileFilter{
          //    sshCommand remote: remote, command: "docker exec e913beeca931 bash -c 'cd /u01/oracle/user_projects/domains/base_domain/bin && . ./setDomainEnv.sh ENV && java weblogic.Deployer -adminurl t3://192.168.100.158:9002 -username '$WEBLOGIC_CREDENTIAL_USR' -password '$WEBLOGIC_CREDENTIAL_PSW' -stop'"
          //   //  }
          //   //  }
          //    }
          //   }
          //  }
         } 
      }
   }
}