pipeline {
    
    agent {
        node {
            label 'master'
        }
    }
    
    tools {
        maven 'maven3'
    }
    
    options {
        buildDiscarder logRotator(
            daysToKeepStr: '15',
            numToKeepStr: '10'
            )
    }
    
    environment {
        APP_NAME = "STUDENT_APP"
        APP_ENV = "DEV"
    }
    
    stages {
        
        stage('Stage 1 - 21051215') {
            steps {
                sh """
                echo "Stage 1 Completed - 21051215"
                """
            }
        }
        
        stage('Parallel Stage') {
            
            parallel {
                
                stage('Stage 2 - 21051215') {
                    steps {
                        pipeline {
                            agent {
                                docker {
                                    container 'stage2-21051215-container'
                                    image 'apache2-21051215-image'
                                }
                            }
                        }
                    }
                }
                
                stage('Stage 3 - 21051215') {
                    steps {
                        sh """
                        echo "Stage 3 Completed - 21051215"
                        """
                    }
                }
            }
        }
        
        stage('Stage 4 - 21051215') {
            steps {
                input('Proceed to release the work?')
            }
        }
        
        stage('Stage 5 - 21051215') {
            when {
                not {
                    branch "Abort"
                }
            }
            steps {
                sh """
                echo "Work Released - 21051215"
                """
            }
        }
    }
}
