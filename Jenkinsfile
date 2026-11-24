pipeline {
    agent any

    stages {
        stage('Validar Estructura N.O.V.A.') {
            steps {
                sh '''
                    set -euo pipefail
                    test -f docker-compose.yml
                    test -f modelfiles/Modelfile
                    test -f .continuerules
                    grep -q "FROM qwen2.5-coder:1.5b" modelfiles/Modelfile
                    grep -q "nova-jenkins" docker-compose.yml
                    grep -q "nova-ollama" docker-compose.yml
                    grep -q "nova-webui" docker-compose.yml
                '''
            }
        }
    }

    post {
        success {
            echo 'Validación de estructura de N.O.V.A. completada sin errores.'
        }
        failure {
            echo 'Fallo en la validación de configuración de N.O.V.A.'
        }
    }
}