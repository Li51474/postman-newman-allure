<<<<<<< HEAD
pipeline {
    agent any

    environment {
        COLLECTION = 'postman\\CRM_API.json'
        ENV_FILE   = 'postman\\CRM_ENV.json'
        DATA_FILE  = 'postman\\data.csv'
        ALLURE_DIR = 'allure-results'
    }

    triggers {
        cron('H 8 * * 1-5')   // 工作日 08:xx
    }

    stages {
        stage('Checkout') {
            steps { checkout scm }
        }

        stage('Install tools') {
            steps {
                // 用 Jenkins 里配好的 NodeJS 工具
                nodejs('NodeJS-18') {
                    bat 'npm install -g newman newman-reporter-allure'
                }
            }
        }

        stage('Run API tests') {
            steps {
                nodejs('NodeJS-18') {
                    bat """
                        newman run %COLLECTION% ^
                          -e %ENV_FILE% ^
                          -d %DATA_FILE% ^
                          -r cli,allure ^
                          --reporter-allure-export %ALLURE_DIR%
                    """
                }
            }
        }

        stage('Publish Allure Report') {
            steps {
                allure([
                    includeProperties: false,
                    reportBuildPolicy: 'ALWAYS',
                    results: [[path: "${ALLURE_DIR}"]]
                ])
            }
        }
    }

    post {
        always {
            emailext subject: "[${env.JOB_NAME}] #${env.BUILD_NUMBER} - ${currentBuild.result ?: 'SUCCESS'}",
                       body: "查看 Allure 报告：${env.BUILD_URL}allure",
                       to: 'your-team@company.com'
        }
    }
}
=======
pipeline {
    agent any

    environment {
        COLLECTION = 'postman\\CRM_API.json'
        ENV_FILE   = 'postman\\CRM_ENV.json'
        DATA_FILE  = 'postman\\data.csv'
        ALLURE_DIR = 'allure-results'
    }

    triggers {
        cron('H 8 * * 1-5')   // 工作日 08:xx
    }

    stages {
        stage('Checkout') {
            steps { checkout scm }
        }

        stage('Install tools') {
            steps {
                // 用 Jenkins 里配好的 NodeJS 工具
                nodejs('NodeJS-18') {
                    bat 'npm install -g newman newman-reporter-allure'
                }
            }
        }

        stage('Run API tests') {
            steps {
                nodejs('NodeJS-18') {
                    bat """
                        newman run %COLLECTION% ^
                          -e %ENV_FILE% ^
                          -d %DATA_FILE% ^
                          -r cli,allure ^
                          --reporter-allure-export %ALLURE_DIR%
                    """
                }
            }
        }

        stage('Publish Allure Report') {
            steps {
                allure([
                    includeProperties: false,
                    reportBuildPolicy: 'ALWAYS',
                    results: [[path: "${ALLURE_DIR}"]]
                ])
            }
        }
    }

    post {
        always {
            emailext subject: "[${env.JOB_NAME}] #${env.BUILD_NUMBER} - ${currentBuild.result ?: 'SUCCESS'}",
                       body: "查看 Allure 报告：${env.BUILD_URL}allure",
                       to: '2149251474@qq.com'
        }
    }
}
>>>>>>> 93edd0b (a)
