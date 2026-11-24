pipeline {
    agent any

    stages {
        stage('Validar Estructura N.O.V.A.') {
            steps {
                sh '''
                    test -f docker-compose.yml
                    test -f modelfiles/Modelfile
                    grep -q "FROM qwen2.5-coder:1.5b" modelfiles/Modelfile
                '''
            }
        }

        stage('Verificar Sintaxis Compose') {
            steps {
                sh 'docker compose config -q'
            }
        }
    }

    post {
        success {
            echo 'Validación del stack N.O.V.A. completada sin errores.'
        }
        failure {
            echo 'Fallo en la validación de configuración de N.O.V.A.'
        }
    }
}