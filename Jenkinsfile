pipeline {

    agent {
      docker { image 'purbon/kafka-topology-builder:latest' }
    }

   stages {
      stage('checkout') {
         steps {
            git branch: 'master', url: 'https://github.com/purbon/kafka-topology-builder-demo.git'
         }
      }
      stage('run') {
          steps {
              withCredentials([usernamePassword(credentialsId: 'confluent-cloud	', usernameVariable: 'CLUSTER_API_KEY', passwordVariable: 'CLUSTER_API_SECRET')]) {
                sh './demo/build-connection-file.sh > topology-builder.properties'
              }
              sh 'kafka-topology-builder.sh  --brokers ${Brokers} --clientConfig topology-builder.properties --topology ${TopologyFiles}'
          }
      }
   }
}
