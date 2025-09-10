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

# 🐳 Combinações Úteis de Comandos Docker

## 🔄 Combinações com Subcomandos ($())

### Remoção em Massa
- docker container rm -f $(docker container ls -qa) → Remove **todos os containers** forçadamente
- docker image rm -f $(docker image ls -q) → Remove **todas as imagens** forçadamente
- docker volume rm $(docker volume ls -q) → Remove **todos os volumes**
- docker network rm $(docker network ls -q) → Remove **todas as redes** não usadas

### Limpeza de Sistema
- docker system prune -f --volumes $(docker system df -q) → Limpeza completa do sistema
- docker container stop $(docker container ls -q) → Para **todos os containers** em execução

### Listagens Filtradas
- docker container ls --filter "name=web" $(docker container ls -q) → Lista containers filtrados
- docker image ls --filter "dangling=true" $(docker image ls -q) → Lista imagens órfãs

## 📋 INFORMAÇÕES E VERSÃO
- docker system info → Informações detalhadas do sistema Docker
- docker builder inspect → Informações do builder
- docker buildx inspect → Inspecionar buildx

## 🏗️ CONSTRUÇÃO DE IMAGENS
- DOCKER_BUILDKIT=1 docker build . → Ativar BuildKit
- docker build --progress=plain . → Modo verbose de build
- docker build --platform linux/amd64,linux/arm64 . → Build multiplataforma
- docker build --no-cache . → Ignorar cache
- docker build --cache-from=image:tag → Usar cache específico
- docker build --metadata-file meta.json . → Exportar metadados

## 🎯 DOCKER COMPOSE AVANÇADO
- docker compose --profile frontend up → Executar com perfil específico
- docker compose --scale web=3 → Escalar serviços
- docker compose --env-file .env.prod up → Usar arquivo env específico

## 🔍 INSPEÇÃO AVANÇADA
- docker system events --format '{{json .}}' → Eventos em JSON
- docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}" → Stats formatados

## 🌐 REDES AVANÇADAS
- docker network create --driver overlay my-network → Rede overlay
- docker network create --subnet 172.20.0.0/16 my-net → Rede com subnet específica

## 🔐 SEGURANÇA
- docker scan minha-imagem → Scan de vulnerabilidades
- docker scan --json minha-imagem → Scan em formato JSON

## ⚡ PERFORMANCE
- docker system df -v → Uso de espaço detalhado
- docker builder prune --all --force → Limpar builder

## 📊 FORMATAÇÃO JSON
- docker ps --format '{{json .}}' → Containers em JSON
- docker images --format '{{.ID}}\t{{.Repository}}' → Imagens formatadas

## 💾 DOCKER COMMIT
- docker commit container_id minha-imagem:tag → Cria imagem a partir do container
- docker commit --author "Nome email" container_id imagem:tag → Especifica autor
- docker commit --message "Descrição" container_id imagem:tag → Adiciona mensagem
- docker commit --change 'ENV DEBUG=true' container_id imagem:tag → Aplica mudanças
- docker commit --change 'WORKDIR /app' container_id imagem:tag → Altera diretório
- docker commit --change 'CMD ["npm", "start"]' container_id imagem:tag → Define comando

## 🐳 COMANDOS SWARM
- docker swarm init → Inicializar swarm
- docker swarm join-token worker → Mostrar token de join
- docker node ls → Listar nodes
- docker service ls → Listar serviços

## 📦 VOLUMES AVANÇADOS
- docker volume create --driver local --opt type=none --opt device=/path/to/data --opt o=bind named-volume → Volume com bind específico

## 🤖 TESTCONTAINERS
- docker run --rm -it -v /var/run/docker.sock:/var/run/docker.sock testcontainers/cloud-local testcontainers config → Configurar Testcontainers

## 🔍 Exemplos de Teste Seguro
bash
# Primeiro veja o que será executado:
- echo $(docker container ls -qa)
- echo $(ps aux | grep 'nginx' | awk '{print $2}')

# Depois execute com confiança:
- docker container rm -f $(docker container ls -qa)

# MySQL

- docker run -d \
    --name mysql-container \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD="senhaForte123!" \
    -e MYSQL_DATABASE=bancodedados \
    -e MYSQL_USER=adminThiago \
    -e MYSQL_PASSWORD=senhaForte456! \
    -v mysql_data:/var/lib/mysql \
    mysql:8.0


_______________________________________________________________________________________

**💡 Dica:** Use `$(comando)` para automatizar tarefas repetitivas, mas **sempre teste com echo primeiro** para evitar acidentes!

_______________________________________________________________________________________

**Nota:** A maioria dos comandos aceita tanto o ID completo quanto os primeiros caracteres (desde que sejam únicos). Use `--help` após qualquer comando para ver opções específicas, exemplo: `docker run --help`.
