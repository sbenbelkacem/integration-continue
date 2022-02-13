node("slave-ic"){

    stage("checkout-catalog"){
        checkout([$class: 'GitSCM', branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sbenbelkacem/catalog']]])
    }

    stage("build"){
        sh "chmod 777 mvnw"
        sh "./mvnw clean package -DskipTests"
        stash includes: 'target/catalog*.jar', name: 'livrable-catalog'
        stash includes: 'Dockerfile', name: 'catalog-dockerfile'
        stash includes: 'docker-compose.yaml', name: 'catalog-dockerfile-compose'
        stash includes: 'launch.sh', name: 'catalog-launch'
    }

    stage("Analyse qualité"){
        sh "./mvnw sonar:sonar \\\n" +
                "  -Dsonar.projectKey=catalog \\\n" +
                "  -Dsonar.host.url=http://54.234.48.131:11001 \\\n" +
                "  -Dsonar.login=1b57cda1577afe576013077f1c941c934f70d52a"

    }
     node("vm-deploy"){
         stage("deploy"){
             unstash 'livrable-catalog'
             unstash 'catalog-dockerfile'
             unstash 'catalog-dockerfile-compose'
             unstash 'catalog-launch'

             sh "chmod 777 launch.sh"
             sh "./launch.sh"

         }
     }






}
