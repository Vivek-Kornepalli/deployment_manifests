def label = "slave"
 
podTemplate(label: label, containers: [
 containerTemplate(name: 'kaniko', image: 'gcr.io/kaniko-project/executor:debug', command: '/busybox/cat', ttyEnabled: true)
],
volumes: [
   secretVolume(mountPath: '/root/.docker/', secretName: 'regcred')
]) {
 node(label) {
   stage('Stage 1: Build with Kaniko') {
     container('kaniko') {
       sh '/kaniko/executor --context=git://github.com/Vivek-Kornepalli/deployment_manifests.git \
               --destination=docker.io/repository/image:tag \
               --insecure \
               --skip-tls-verify  \
               -v=debug'
     }
   }
 }
}