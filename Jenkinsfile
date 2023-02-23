def label = "slave"
podTemplate(label: label, containers:[
 containerTemplate(name: 'kaniko', image: 'gcr.io/kaniko-project/executor:debug', command: '/busybox/cat', ttyEnabled: true)
]){
 node(label) {
   stage('Stage 1: Build with Kaniko'){
     container('kaniko'){
       sh '/kaniko/executor --context=git://github.com/Vivek-Kornepalli/deployment_manifests.git \
               --destination=registry.digitalocean.com/metaphy:latest \
               --insecure \
               --skip-tls-verify  \
               -v=debug'
     }
   }
 }
}