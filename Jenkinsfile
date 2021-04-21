pipeline{
    tools{
        jdk 'myjava'
        mvn 'mymaven'
        
    }
    agent none
    stages{
        stage('checkout'){
            agent any
            steps{
                git 'https://github.com/subhasish5543/DevOpsClassCodes.git'
            }
        }
        stage('compile'){
            agent {label 'linux_slave'}
            steps{
                git 'https://github.com/subhasish5543/DevOpsClassCodes.git'
                sh 'mvn compile'
                
            }
        
        }
        stage ('codereview'){
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
                agent {label 'win_slave'}
                steps{
                    git 'https://github.com/devops-trainer/DevOpsClassCodes.git'
                    bat 'mvn test'
                }
                
            }
            stage('MetriCheck'){
                agent any
                steps{
                    sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
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
