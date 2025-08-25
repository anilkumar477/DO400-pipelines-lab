pipeline{
    agent any

    parameters{
        booelanParam(name: "RUN_INTEGRATION_TESTS", defaultValue: true)
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
                        steps{
                            sh './mvnw test -d testGroups=integration'
                        }
                    }
                
            }
        }
    }
}