pipeline{
    tools{
         maven 'mymaven'
    }
    agent any
        stages{
            stage('checkout'){ 
                agent any
                steps{
                    git 'https://github.com/mahidev29/Devopsclasscodes.git'
            }
                     }
            
             stage('Compile'){
                agent any
                steps{
                    sh 'mvn compile'
                }
                
            }
            stage('CodeReview'){
                agent any
                steps{
                    sh 'mvn pmd:pmd'
                }
                post{
                    always{
                        pmd pattern: 'target/pmd.xml'
                    }
                }
            }
            stage('UnitTest'){
                agent any
                steps{
                    sh 'mvn test'
                }
                
            }
            stage('MetriCheck'){
                 agent {label 'Win_slave1'}
                steps{
                    git 'https://github.com/mahidev29/Devopsclasscodes.git'
                    bat 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
                }
                post{
                    always{
                        cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                    }
                }
            }
            stage('Package'){
                agent any
                steps{
                    sh 'mvn package'
                }
            }
            
        }
    
    }        
    
