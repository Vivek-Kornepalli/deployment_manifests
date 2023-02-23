def label = "kube-agent"
podTemplate(label: label, 
containers: [
                            containerTemplate(
                                name: 'kaniko',
                                image: 'registry.digitalocean.com/metaphy/kaniko:v2',
                                command: 'sleep',
                                args: '99d',
                                ttyEnabled: true,
                                imagePullSecrets: {name: 'regcred'}
                            )
                        ])
{
 node(label) {
   stage('Stage 1: Build with Kaniko'){

     container('kaniko'){
       sh '''
       sleep 30
       /kaniko/executor --force -f Dockerfile --context=git://github.com/Vivek-Kornepalli/deployment_manifests.git \
               --destination=registry.digitalocean.com/metaphy:latest \
               --insecure \
               --skip-tls-verify  \
               -v=debug
          '''
     }
   }
 }
}

