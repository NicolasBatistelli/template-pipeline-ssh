pipeline {
    parameters {
        string(name: 'BRANCH', description: 'Enter the name of the branch to deploy')
    }
    agent any
    stages {
        stage("Build Info") {
            steps {
                script {
                    BUILD_TRIGGER_BY = currentBuild.getBuildCauses()[0].userId
                    currentBuild.displayName = "#${env.BUILD_NUMBER} Branch: ${Branch} By: ${BUILD_TRIGGER_BY}"
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    Branch = params.BRANCH
                    try {
                        // Comando SSH para ejecutar el script remoto
                        def result = sh(script: "ssh user@ip sh ruta/deploy.sh ${Branch}", returnStatus: true)

                        // Verificar el código de salida del comando SSH
                        if (result != 0) {
                            error("Error: El comando SSH no se ejecutó correctamente. Código de salida: ${result}")
                        }
                    } catch (Exception ex) {
                        // Capturar cualquier excepción y manejarla
                        error("Error durante la ejecución del script: ${ex.message}")
                    }
                }
            }
        }
    }
}
