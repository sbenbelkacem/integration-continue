node("slave-ic"){

    stage("checkout-catalog"){
        checkout([$class: 'GitSCM', branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sbenbelkacem/catalog']]])
    }

}
