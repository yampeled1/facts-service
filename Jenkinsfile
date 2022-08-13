podTemplate(label: 'service-demo', cloud: 'kubernetes', serviceAccount: 'yamp-jenkins',
  containers: [
    containerTemplate(name: 'docker', image: 'docker:git', ttyEnabled: true, command: 'cat', privileged: true)
  ],
  volumes: [
    hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')
  ]) {
    node('service-demo') {
        stage('Build Docker Image') {
            withCredentials([usernamePassword(credentialsId: 'docker-creds',
                                  usernameVariable: 'USER', 
                                  passwordVariable: 'PASS')]) {
            container('docker') {
                sh """
                  docker build -t time-service:$BUILD_NUMBER .
                """
            }
          }
        }
    }
}
