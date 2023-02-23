def label = "kube-agent"
podTemplate(label: label, 
containers: [
                            containerTemplate(
                                name: 'kaniko',
                                image: 'registry.digitalocean.com/metaphy/kaniko:v3',
                                command: 'sleep',
                                args: '99d',
                                ttyEnabled: true
                            )
                        ], imagePullSecrets: ['regcred'])
{
 node(label) {
   stage('Stage 1: Build with Kaniko'){

     container('kaniko'){
       sh '''
       /kaniko/executor --force -f Dockerfile --context=git://github.com/Vivek-Kornepalli/deployment_manifests.git \
               --destination=registry.digitalocean.com/metaphy/kaniko:node-test-v1 \
               --insecure \
               --skip-tls-verify  \
               -v=debug
          '''
     }
   }
 }
}

