pipeline{
    agent any
    tools {
        maven 'Maven'
    }
    stages{
        stage("Test"){
            steps{
                slackSend channel: 'testing', message: 'Job Started'
                sh 'mvn test'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    slackSend channel: 'testing', message: 'Success'
                }
                failure{
                    slackSend channel: 'testing', message: 'Failed'
                }
            }
        }
        stage("Build"){
            steps{
                sh 'mvn package'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    slackSend channel: 'testing', message: 'Success'
                }
                failure{
                    slackSend channel: 'testing', message: 'Failed'
                }
            }
        }
        stage("Deploy To Test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcatdetail', path: '', url: 'http://3.17.36.113:8080/')], contextPath: '/app', war: '**/*.war'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    slackSend channel: 'testing', message: 'Success'
                }
                failure{
                    slackSend channel: 'testing', message: 'Failed'
                }
            }
        }
        stage("Deploy To Prod"){
             input {
                message "Should we continue?"
                ok "Yes"
            }
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcatdetail', path: '', url: 'http://18.218.3.44:8080/')], contextPath: '/app', war: '**/*.war'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    slackSend channel: 'testing', message: 'Success'
                }
                failure{
                    slackSend channel: 'testing', message: 'Failed'
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            slackSend channel: 'testing', message: 'Success'
        }
        failure{
            slackSend channel: 'testing', message: 'Failed'
        }
    }
}
