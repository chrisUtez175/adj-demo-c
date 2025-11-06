pipeline{
    agent any

    stages{
        // Para todo los servicios      
        stage('Para todos los servicios'){
            steps{
                sh'''
                    docker compose -p adj-demo down || true
                '''
            }
        }

        //para eliminar imagene anteriores

        stage('Borrando imagenes antiguas'){
            steps{
                sh'''
                    IMAGES=$(docker images --filter "label=com.docker.compose.project=adj-demo" -q)
                    if[ -n '$IMAGES']; then
                        docker images rmi $IMAGES
                    else
                        echo "No hay imagenes para borrar"
                    fi  
                '''
            }

        }
        //bajar la actualizacion
        
        stage('Actualizado...'){
            steps{
                checkout scm
            }
        }
    
        //levantar y desplegar el proyecto
        stage('Construyendo y desplegando...'){
            steps{
                sh'''
                    docker compose up --build -d
                '''
            }
        }
    }

    post{
        success{
            echo 'pipeline ejecutada correctamente'
        }

        failure{
            echo 'Error al ejecutar la pipeline'
        }
        
        always{
            echo 'Finalizo la ejecucion de la pipeline'
        }
    }
}