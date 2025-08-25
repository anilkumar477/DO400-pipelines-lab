pipeline{
    agent any

    parameters{
        booleanParam(name: "RUN_INTEGRATION_TESTS", defaultValue: true)
    }
    stages{
        stage('Test'){
            parallel{
                stage('Unit tests'){
                    steps{
                        sh './mvnw test -D testGroups=unit'
                    }
                }
                stage('Integration tests'){
                        when{
                            expression{ return params.RUN_INTEGRATION_TESTS}
                        }
                        
                    }
                
            }
        }
        stage('Build'){
            steps{
                script{
                    try{
                        sh './mvnw test -D testGroups=integration'
                    }catch(ex){
                        echo "Error while enerationg JAR file"
                        throw ex
                        }
                }
            }

        }
    }
}