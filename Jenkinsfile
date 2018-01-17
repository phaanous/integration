pipeline {
    agent any

    parameters {        
        string(name: 'TIER_ONE_BRANCH', defaultValue: '', description: 'The tier one branch name to build')
        string(name: 'TIER_TOW_BRANCH', defaultValue: '', description: 'The tier two branch name to build')
        string(name: 'TIER_THREE_BRANCH', defaultValue: '', description: 'The tier three branch name to build')
    }

    stages {

        stage('Trigger builds on all tiers in parallel') {                        

            failFast true

            parallel {

                stage ('Build tier one'){

                    steps {
                        build job: "OPG-J2-EXP-FEATURE-BUILD/OPG-J2-EXP-TIER-ONE-FEATURE/${env.TIER_ONE_BRANCH}", 
                            propagate: true, 
                            wait: true,
                            parameters: [                        
                                    [$class: 'StringParameterValue', name: 'BRANCH_TO_BUILD', value: env.TIER_ONE_BRANCH]
                                ]
                        echo "Completed building tier one's ${env.TIER_ONE_BRANCH} branch"
                    }        

                }

                stage ('Build tier two'){

                    steps {
                        build job: "OPG-J2-EXP-FEATURE-BUILD/OPG-J2-EXP-TIER-ONE-FEATURE/${env.TIER_TWO_BRANCH}", 
                            propagate: true, 
                            wait: true,
                            parameters: [                        
                                    [$class: 'StringParameterValue', name: 'BRANCH_TO_BUILD', value: env.TIER_TWO_BRANCH]
                                ]
                        echo "Completed building tier two's ${env.TIER_TWO_BRANCH} branch"
                    }        

                }

                stage ('Build tier tree'){

                    steps {
                        build job: "OPG-J2-EXP-FEATURE-BUILD/OPG-J2-EXP-TIER-ONE-FEATURE/${env.TIER_THREE_BRANCH}", 
                            propagate: true, 
                            wait: true,
                            parameters: [                        
                                    [$class: 'StringParameterValue', name: 'BRANCH_TO_BUILD', value: env.TIER_THREE_BRANCH]
                                ]
                        echo "Completed building tier three's ${env.TIER_THREE_BRANCH} branch"
                    }        

                }

            }
            
        }

        stage('Run Integration Tests') {
            steps {
                echo 'Testing..'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}