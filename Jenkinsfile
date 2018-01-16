pipeline {
    agent any

    parameters {        
        string(name: 'FRONT_END_BRANCH', defaultValue: '', description: 'The front end branch to build')
        string(name: 'BACK_END_BRANCH', defaultValue: '', description: 'The back end branch to build')
        string(name: 'AUTH_MEMBRANE_BRANCH', defaultValue: '', description: 'The membrane branch to build')
    }

    stages {
        stage('Trigger feature build job on tier one') {                        
            steps {
                build job: 'OPG-J2-EXP-FEATURE-BUILD/OPG-J2-EXP-TIER-ONE-FEATURE/feature-123', 
                propagate: true, 
                wait: true,
                parameters: [
                        [$class: 'StringParameterValue', name: 'FEATURE_BUILD', 'value': 'true'], 
                        [$class: 'StringParameterValue', name: 'BRANCH_TO_BUILD', value: env.AUTH_MEMBRANE_BRANCH]
                    ]
            }        
        }
        stage('Test') {
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