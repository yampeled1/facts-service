podTemplate(label: 'service-demo', cloud: 'kubernetes', serviceAccount: 'yamp-jenkins',
  containers: [
    containerTemplate(name: 'docker', image: 'docker:git', ttyEnabled: true, command: 'cat', privileged: true,
        envVars: [secretEnvVar(key: 'DOCKER_CREDS', secretName: 'docker-creds', secretKey: 'password'),
    ])
  ],
  volumes: [
    secretVolume(secretName: 'docker-hub-credentials', mountPath: '/etc/.secret'),
    hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')
  ]) {
    node('demo-customer-pod') {
        stage('Build Docker Image') {
            container('docker') {
                sh """
                  docker build -t time-service:$BUILD_NUMBER .
                """
            }
        }
    }
}