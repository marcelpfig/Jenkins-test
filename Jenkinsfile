def remote = [:]
remote.name = 'ansible2'
remote.host = '192.168.122.52'
remote.allowAnyHosts = true


pipeline {
    stages {
        withCredentials([sshUserPrivateKey(credentialsId: 'ssh-private-key', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'root')]) {
        remote.user = userName
        remote.identityFile = identity
            stage("SSH Steps Rocks!") {
                writeFile file: 'abc.sh', text: 'ls'
                sshCommand remote: remote, command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
                sshPut remote: remote, from: 'abc.sh', into: '.'
                sshGet remote: remote, from: 'abc.sh', into: 'bac.sh', override: true
                sshScript remote: remote, script: 'abc.sh'
                sshRemove remote: remote, path: 'abc.sh'
            }
        }   
    }
}