node('docker-slave'){
    
    properties([
      parameters(
        [
            string(defaultValue: '3.9.30-1', description: 'origin version', name: 'VERSION'),
            string(defaultValue: 'talitabp/origin-ansible', description: 'openshift-ansible version', name: 'PREFIX'),
            string(defaultValue: 'v3.9', description: 'openshift-ansible version', name: 'OS_TAG'),
            string(defaultValue: 'v3.9', description: 'openshift-ansible version', name: 'OS_PUSH_TAG'),


                                
                                
        ],
      ),      
   
    ])
   ansiColor('xterm') {
        timestamps {
            
             
          
            stage ('Build Image'){
                 
                 
                sh """
                   curl -OL https://github.com/openshift/openshift-ansible/archive/openshift-ansible-${VERSION}.tar.gz
                   tar xzvf openshift-ansible-${VERSION}.tar.gz
                   cd openshift-ansible-openshift-ansible-${VERSION}/
                   ./hack/build-images.sh
                   
                """
             }

            stage ('Push Image'){
                
              withDockerRegistry([credentialsId: '5526303b-ca3a-4c19-8051-1c23b8cba806', url: 'https://index.docker.io/v1/']) {
                sh """

                   ./hack/push-release.sh

                """
              }
            }
         } 
        
        
   }
    
}