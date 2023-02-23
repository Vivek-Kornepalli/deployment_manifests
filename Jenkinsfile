def label = "slave"

 
podTemplate(label: label, containers: [
 containerTemplate(name: 'kaniko', image: 'gcr.io/kaniko-project/executor:debug', command: '/busybox/cat', ttyEnabled: true)
],
volumes: [
   secretVolume(mountPath: '/root/.docker/', secretName: 'regcred')
]){
 node(label) {

  // stages{
  //   stage("Building Clone"){

  //   }
  // }


   stage('Stage 1: Build with Kaniko') {
     container('kaniko') {
       sh '/kaniko/executor --context=git://github.com/Vivek-Kornepalli/deployment_manifests.git \
               --destination=registry.digitalocean.com/metaphy:${BUILD_NUMBER} \
               --insecure \
               --skip-tls-verify  \
               -v=debug'
     }
   }
 }
}