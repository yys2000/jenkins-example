pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
              
                    sh 'mvn clean compile'
              
            }
        }

        stage ('Testing Stage') {

            steps {
               
                    sh 'mvn test'
               
            }
        }

        stage ('Deploy?') {
            steps {
                input('Do you want to deploy?')
            }
        }

        stage ('Deployment Stage') {
            steps {

		            withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'PCF_LOGIN',
                            usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {

                    sh '/usr/local/bin/cf login -a http://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
			        sh '/usr/local/bin/cf push'

			
                }
            }
        }
    }
}
