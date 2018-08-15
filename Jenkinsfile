node {
    def remote = [:]
    remote.name = 'test'
    remote.allowAnyHosts = true
    remote.host = '192.168.2.5'
    remote.user = 'root'
    remote.port = 2122
    remote.identity = credentials('bae24a1e-e9f6-44c8-9d51-bdb42cf4bd60')

    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'e2068618-67f0-4edb-925e-a7aa7c7a4bad', name: 'acv-hoanx', url: 'https://github.com/acv-hoanx/test-laravel-cicd.git']]])

    stage('Build') {
      sh 'printenv'
    }
}