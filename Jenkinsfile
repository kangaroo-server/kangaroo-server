/**
 * Jekyll check pipeline for our documentation site.
 */

pipeline {

    agent { label 'worker' }

    options {
        timeout(time: 30, unit: 'MINUTES')
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    stages {

        /**
         * Get environment statistics.
         */
        stage('Stat') {
            steps {
                script {
                    sh 'env'
                    sh 'ruby --version'
                    sh 'gem --version'
                    sh 'bundle --version'
                }
            }
        }

        /**
         * Install.
         */
        stage('Install') {
            steps {
                sh 'bundle install'
            }
        }

        /**
         * Test and build.
         */
        stage('Test') {
            steps {
                parallel(
                        'test': {
                            sh("bundle exec jekyll doctor")
                        },
                        'build': {
                            sh("bundle exec jekyll build")
                        },
                        failFast: false
                )
            }
        }
    }

    post {

        /**
         * When the build status changed, send the result.
         */
        changed {
            script {
                def buildStatus = currentBuild.currentResult
                def url = env.BUILD_URL, message, color

                if (env.CHANGE_URL && buildStatus == 'SUCCESS') {
                    url = env.CHANGE_URL
                }

                switch (buildStatus) {
                    case 'FAILURE':
                        message = "Build <${url}|${env.JOB_NAME}> failed."
                        color = '#AA0000'
                        break
                    case 'SUCCESS':
                        message = "Build <${url}|${env.JOB_NAME}> passed."
                        color = '#00AA00'
                        break
                    case 'UNSTABLE':
                    default:
                        message = "Build <${url}|${env.JOB_NAME}> unstable."
                        color = '#FFAA00'
                }

                slackSend(
                        channel: '#build-notifications',
                        tokenCredentialId: 'kangaroo-server-slack-id',
                        teamDomain: 'kangaroo-server',
                        color: color,
                        message: message
                )
            }
        }

        /**
         * Actions always to run at the end of a pipeline.
         */
        always {
            /**
             * Delete everything, to keep track of disk size.
             */
            cleanWs(deleteDirs: true)
        }
    }
}
