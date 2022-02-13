node("slave-ic"){

    stage("checkout-catalog"){
        checkout([$class: 'GitSCM', branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sbenbelkacem/catalog']]])
    }

    stage("build"){
        sh "chmod 777 mvnw"
        sh "./mvnw clean package -DskipTests"
    }

}
