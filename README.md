# 🐳 Lista de Comandos do Docker Engine

## 📋 Informações e Versão
- docker version → Exibe a versão do Docker instalada
- docker info → Mostra informações detalhadas do sistema Docker
- docker system df → Exibe o uso de espaço em disco do Docker

## 🐳 Gerenciamento de Containers

### Executando Containers
- docker run [opções] imagem [comando] → Executa um container a partir de uma imagem
- docker run -d --name meu_container nginx → Executa container em segundo plano
- docker run -it ubuntu /bin/bash → Executa container interativo
- docker run -p 8080:80 nginx → Mapeia porta do host para o container
- docker run -v /host/path:/container/path nginx → Monta volume

### Listando e Monitorando
- docker ps → Lista containers em execução
- docker ps -a → Lista todos os containers (incluindo parados)
- docker stats → Mostra estatísticas em tempo real dos containers
- docker top container_id → Mostra processos em execução no container
- docker logs container_id → Exibe logs do container
- docker logs -f container_id → Segue logs em tempo real

### Gerenciando Containers
- docker start container_id → Inicia um container parado
- docker stop container_id → Para um container em execução
- docker restart container_id → Reinicia um container
- docker pause container_id → Pausa um container
- docker unpause container_id → Despausa um container
- docker rm container_id → Remove um container parado
- docker rm -f container_id → Força remoção de container em execução
- docker exec -it container_id /bin/bash → Executa comando em container running
- docker attach container_id → Conecta ao terminal do container

## 🏞️ Gerenciamento de Imagens

### Buscando e Baixando
- docker search termo → Busca imagens no Docker Hub
- docker pull imagem:tag → Baixa imagem do registry
- docker images → Lista imagens locais
- docker image ls → Lista imagens (formato mais recente)

### Construindo Imagens
- docker build -t minha-imagem:tag . → Constrói imagem do Dockerfile
- docker build -f Dockerfile.dev . → Constrói usando Dockerfile específico
- docker history imagem_id → Mostra histórico de camadas da imagem

### Gerenciando Imagens
- docker tag imagem_id novo_nome:tag → Adiciona tag à imagem
- docker push usuario/imagem:tag → Envia imagem para registry
- docker rmi imagem_id → Remove imagem local
- docker rmi -f imagem_id → Força remoção de imagem
- docker image prune → Remove imagens não utilizadas

## 🔗 Redes e Volumes

### Gerenciamento de Redes
- docker network ls → Lista redes disponíveis
- docker network create minha_rede → Cria uma nova rede
- docker network inspect minha_rede → Inspeciona rede
- docker network connect rede container → Conecta container à rede
- docker network disconnect rede container → Desconecta container da rede
- docker network rm minha_rede → Remove rede

### Gerenciamento de Volumes
- docker volume ls → Lista volumes
- docker volume create meu_volume → Cria volume
- docker volume inspect meu_volume → Inspeciona volume
- docker volume rm meu_volume → Remove volume
- docker volume prune → Remove volumes não utilizados

## 🧹 Limpeza e Manutenção
- docker system prune → Remove containers, imagens e networks não utilizados
- docker system prune -a → Remove todos os recursos não utilizados
- docker container prune → Remove containers parados
- docker image prune → Remove imagens não utilizadas
- docker volume prune → Remove volumes não utilizados
- docker network prune → Remove networks não utilizadas

## 🔍 Inspeção e Debug
- docker inspect recurso_id → Mostra informações detalhadas de qualquer recurso
- docker diff container_id → Mostra arquivos modificados no container
- docker cp container_id:/caminho/arquivo . → Copia arquivo do container para host
- docker cp arquivo container_id:/caminho/ → Copia arquivo do host para container
- docker port container_id → Mostra portas mapeadas do container

## 🐳 Docker Compose (Complementar)
- docker-compose up → Inicia serviços definidos no docker-compose.yml
- docker-compose up -d → Inicia serviços em segundo plano
- docker-compose down → Para e remove serviços
- docker-compose ps → Lista serviços do compose
- docker-compose logs → Mostra logs dos serviços
- docker-compose build → Constrói imagens dos serviços

## ⚙️ Configuração do Daemon
- docker events → Mostra eventos do Docker em tempo real
- docker login → Faz login no Docker Hub
- docker logout → Faz logout do Docker Hub

## 🚨 Comandos Úteis para Troubleshooting
- docker run --rm -it alpine sh → Container temporário para testes
- docker run --rm busybox ping google.com → Teste de conectividade
- docker run --rm -v /var/run/docker.sock:/var/run/docker.sock docker → Docker in Docker

_______________________________________________________________________________________

**Nota:** A maioria dos comandos aceita tanto o ID completo quanto os primeiros caracteres (desde que sejam únicos). Use `--help` após qualquer comando para ver opções específicas, exemplo: `docker run --help`.
