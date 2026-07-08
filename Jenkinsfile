pipeline {
    agent any

    stages {
        stage('Clonar Repositório') {
            steps {
                checkout scm
            }
        }

        stage('Deploy no Swarm') {
            steps {
                echo "Efetuando deploy da stack 'crm' (Evo CRM Community) no Swarm..."
                sh """
                    # Carrega as variáveis do .env central da VPS para rodar o stack deploy
                    if [ -f /root/.env ]; then
                        set -a
                        . /root/.env
                        set +a
                    fi
                    
                    docker stack deploy -c docker-compose.yml crm
                """
            }
        }
    }

    post {
        success {
            echo "Sucesso! A stack 'crm' foi implantada e atualizada com sucesso."
        }
        failure {
            echo "Falha! Ocorreu um erro no deploy da stack 'crm'. Verifique os logs."
        }
    }
}
