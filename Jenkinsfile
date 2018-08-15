node {
    def remote = [:]
    remote.name = 'test'
    remote.allowAnyHosts = true
    remote.host = '192.168.2.5'
    remote.user = 'root'
    remote.port = 2122
    remote.identity = credentials('bae24a1e-e9f6-44c8-9d51-bdb42cf4bd60')

    stage('Build') {
      sshCommand remote: remote, command: "ls -lrt"
    }
}