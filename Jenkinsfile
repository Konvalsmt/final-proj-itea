stageResultMap = [:]

pipeline {
    agent any
    parameters {
        choice(
            choices: ['greeting' , 'silence'],
            description: '',
            name: 'REQUESTED_ACTION')
    }
 
    stages {
        
        stage('A') {
            steps {
                println("This is stage: ${STAGE_NAME}")
            }
        }
        
        stage('Check if exist structure') {
                            steps {
                                script {
                                    // Catch exceptions, set the stage result as unstable,
                                    // build result as failure, and the variable didB1Succeed to false
                                    try {                                        
                                        sh "cp ../inventory /ansible-itea/inventory"
                                        stageResultMap.didB1Succeed = false
                                    }
                                    catch (Exception e) {
                                        // currentBuild.result = 'FAILURE'
                                        stageResultMap.didB1Succeed = true                                        
                                    }
                                }
                            }
                        }
            
                         stage('C1') {
                            // Execute only if B1 succeeded
                            when {
                                expression {
                                    return stageResultMap.find{ it.key == "didB1Succeed" }?.value
                                }
                            }
                            steps {
                               // script {
                                // Mark the stage and build results as failure on error but continue pipeline execution
                                //catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                                    sh "echo Hello"
                                //}
                            }
                        }
    }                  
                        
}

