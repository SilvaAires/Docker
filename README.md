# 🐳 **Guia Completo de Comandos Docker Engine (Ubuntu 24.04.3 LTS)**

---

## 📋 **Informações e Versão**

* `docker version` → Exibe versão cliente/servidor
* `docker info` → Mostra detalhes do sistema Docker
* `docker system info` → Informações completas do sistema
* `docker system df [-v]` → Uso de disco (detalhado com `-v`)
* `docker builder inspect` → Info sobre o builder
* `docker buildx inspect` → Info sobre buildx

---

## 🐳 **Gerenciamento de Containers**

### 🚀 Executando Containers

* `docker run [opções] imagem [comando]` → Cria e executa container
* `docker run -d --name meu_container nginx` → Em segundo plano
* `docker run -it ubuntu /bin/bash` → Interativo
* `docker run -p 8080:80 nginx` → Mapear porta
* `docker run -v /host:/container nginx` → Montar volume
* `docker run --rm alpine sh` → Remove ao sair

### 📊 Listando e Monitorando

* `docker ps` → Lista containers ativos
* `docker ps -a` → Todos containers
* `docker ps --filter "status=exited"` → Filtro de estado
* `docker stats` → Estatísticas em tempo real
* `docker top container_id` → Processos no container
* `docker logs container_id` → Logs
* `docker logs -f container_id` → Logs em tempo real
* `docker logs --tail 100 container_id` → Últimas 100 linhas

### ⚙️ Gerenciando Containers

* `docker start container_id` → Inicia parado
* `docker stop container_id` → Para
* `docker restart container_id` → Reinicia
* `docker pause/unpause container_id` → Pausa/despausa
* `docker rm container_id` → Remove parado
* `docker rm -f container_id` → Força remoção
* `docker exec -it container_id /bin/bash` → Executa comando dentro
* `docker attach container_id` → Conecta terminal

### 📦 Export/Import Containers

* `docker export container_id > container.tar` → Exporta container
* `docker import container.tar` → Importa como imagem

### 🧩 Checkpoint e Restore (Experimental)

* `docker checkpoint create container_id meu_checkpoint` → Cria checkpoint
* `docker start --checkpoint meu_checkpoint container_id` → Restaura container

---

## 🏞️ **Gerenciamento de Imagens**

### 🔍 Buscando e Baixando

* `docker search termo` → Busca no Hub
* `docker pull imagem:tag` → Baixa imagem
* `docker images` ou `docker image ls` → Lista imagens
* `docker images --filter dangling=true` → Apenas órfãs

### 🏗️ Construindo Imagens

* `docker build -t minha-imagem:tag .` → Constrói imagem
* `docker build -f Dockerfile.dev .` → Dockerfile específico
* `DOCKER_BUILDKIT=1 docker build .` → Ativa BuildKit
* `docker build --no-cache .` → Ignora cache
* `docker build --platform linux/amd64,linux/arm64 .` → Multiplataforma
* `docker history imagem_id` → Histórico

### 🗂️ Gerenciando Imagens

* `docker tag imagem_id novo_nome:tag` → Adiciona tag
* `docker push usuario/imagem:tag` → Envia ao registry
* `docker rmi imagem_id` → Remove local
* `docker rmi -f imagem_id` → Força remoção
* `docker image prune` → Remove não utilizadas
* `docker save -o arquivo.tar imagem:tag` → Exporta imagem
* `docker load -i arquivo.tar` → Importa imagem

---

## 🔗 **Redes e Volumes**

### 🌐 Redes

* `docker network ls` → Lista redes
* `docker network create minha_rede` → Cria rede
* `docker network inspect minha_rede` → Inspeciona
* `docker network connect rede container` → Conecta container
* `docker network disconnect rede container` → Desconecta
* `docker network rm minha_rede` → Remove rede
* `docker network create --driver overlay minha_rede` → Overlay
* `docker network create --subnet 172.20.0.0/16 minha_rede` → Subnet

### 💾 Volumes

* `docker volume ls` → Lista volumes
* `docker volume create meu_volume` → Cria volume
* `docker volume inspect meu_volume` → Inspeciona
* `docker volume rm meu_volume` → Remove
* `docker volume prune` → Remove não usados
* `docker volume create --driver local --opt type=none --opt device=/path/to/data --opt o=bind nome` → Volume bind

---

## 🧹 **Limpeza e Manutenção**

* `docker system prune` → Remove não usados
* `docker system prune -a` → Remove todos não usados
* `docker container prune` → Remove parados
* `docker image prune` → Remove imagens órfãs
* `docker volume prune` → Volumes não usados
* `docker network prune` → Redes não usadas
* `docker builder prune --all --force` → Limpa cache build

---

## 🔍 **Inspeção e Debug**

* `docker inspect recurso_id` → Informações detalhadas
* `docker diff container_id` → Arquivos modificados
* `docker cp container_id:/arquivo .` → Copia do container
* `docker cp arquivo container_id:/path/` → Copia para container
* `docker port container_id` → Portas mapeadas
* `docker events` → Eventos em tempo real
* `docker system events --format '{{json .}}'` → Eventos em JSON

---

## 🐳 **Docker Compose**

* `docker compose up` → Inicia serviços
* `docker compose up -d` → Inicia em segundo plano
* `docker compose down` → Para e remove serviços
* `docker compose ps` → Lista serviços
* `docker compose logs` → Logs dos serviços
* `docker compose build` → Constrói imagens
* `docker compose --scale web=3` → Escala serviço
* `docker compose --profile frontend up` → Perfil específico
* `docker compose --env-file .env.prod up` → Arquivo env

---

## 🔐 **Segurança e Registry**

* `docker login` / `docker logout` → Hub oficial
* `docker login registry.meuservidor.com` → Registry privado
* `docker scan minha-imagem` → Scan vulnerabilidades
* `docker scan --json minha-imagem` → Saída JSON

---

## ⚡ **Avançados**

### 🐳 Commit

* `docker commit container_id minha-imagem:tag` → Cria imagem
* `docker commit --author "Nome" --message "Descrição" container_id imagem:tag` → Detalhado
* `docker commit --change 'CMD ["npm", "start"]' container_id imagem:tag` → Modifica config

### 🐳 Swarm

* `docker swarm init` → Inicializa cluster
* `docker swarm join-token worker` → Token de join
* `docker node ls` → Lista nós
* `docker service ls` → Lista serviços
* `docker stack deploy -c docker-compose.yml mystack` → Deploy de stack
* `docker stack ps mystack` → Processos da stack
* `docker stack rm mystack` → Remove stack

---

## 📊 **Formatação de Saída**

* `docker ps --format '{{json .}}'` → Saída JSON
* `docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}’` → Estatísticas formatadas
* `docker images --format '{{.ID}}\t{{.Repository}}'` → Lista formatada

---

## 🚨 **Troubleshooting**

* `docker run --rm busybox ping google.com` → Teste rede
* `docker run --rm -it -v /var/run/docker.sock:/var/run/docker.sock docker` → Docker-in-Docker
* `docker container stop $(docker ps -q)` → Para todos
* `docker container rm -f $(docker ps -qa)` → Remove todos
* `docker image rm -f $(docker images -q)` → Remove todas imagens

---

## 🐳 **Exemplo: MySQL**

```bash
docker run -d \
  --name mysql-container \
  -p 3306:3306 \
  -e MYSQL_ROOT_PASSWORD="senhaForte123!" \
  -e MYSQL_DATABASE=bancodedados \
  -e MYSQL_USER=adminThiago \
  -e MYSQL_PASSWORD=senhaForte456! \
  -v mysql_data:/var/lib/mysql \
  mysql:8.0
```

---

💡 **Dica:** sempre teste comandos de massa com `echo $(...)` antes de executar.
📌 **Nota:** qualquer comando pode ser detalhado com `--help`.

---

# 📑 O que consta na **documentação oficial do Docker Engine**

### 🔹 1. Comandos principais de **containers**

* `docker create` – cria um novo container mas não o inicia.
* `docker start` – inicia um ou mais containers parados.
* `docker run` – cria e inicia um container.
* `docker exec` – executa um comando em um container em execução.
* `docker ps` – lista containers.
* `docker stop` – para um ou mais containers.
* `docker kill` – envia sinal para containers.
* `docker restart` – reinicia um ou mais containers.
* `docker rm` – remove containers.
* `docker pause` / `docker unpause` – pausa ou retoma processos dentro de containers.
* `docker attach` – anexa seu terminal a um container.
* `docker wait` – bloqueia até o container parar, retornando o código de saída.
* `docker export` – exporta o sistema de arquivos de um container como tar.
* `docker import` – importa um tar para criar uma imagem.
* `docker cp` – copia arquivos entre host e container.
* `docker commit` – cria uma nova imagem a partir de um container.

---

### 🔹 2. Comandos principais de **imagens**

* `docker build` – constrói uma imagem a partir de um Dockerfile.
* `docker pull` – baixa uma imagem de um registry.
* `docker push` – envia uma imagem para um registry.
* `docker images` – lista imagens.
* `docker rmi` – remove imagens.
* `docker save` – salva uma imagem em arquivo tar.
* `docker load` – carrega imagem a partir de arquivo tar.
* `docker tag` – marca uma imagem com outro nome.
* `docker history` – mostra histórico de camadas de uma imagem.
* `docker inspect` – mostra detalhes de imagens ou containers.

---

### 🔹 3. Comandos de **volumes**

* `docker volume create`
* `docker volume ls`
* `docker volume inspect`
* `docker volume rm`
* `docker volume prune`

---

### 🔹 4. Comandos de **redes**

* `docker network create`
* `docker network ls`
* `docker network inspect`
* `docker network connect`
* `docker network disconnect`
* `docker network rm`
* `docker network prune`

---

### 🔹 5. Comandos de **sistema**

* `docker info` – exibe informações detalhadas sobre o sistema Docker.
* `docker version` – mostra versão do client/daemon.
* `docker system df` – mostra uso de disco.
* `docker system prune` – limpa recursos não usados.

---

### 🔹 6. **Swarm mode**

* `docker swarm init` / `docker swarm join`
* `docker swarm leave`
* `docker node ls` / `docker node inspect`
* `docker service create` / `docker service ls` / `docker service ps` / `docker service rm`
* `docker stack deploy` / `docker stack services` / `docker stack rm` / `docker stack ps`

---

### 🔹 7. **Configurações e secrets**

* `docker config create` / `docker config ls` / `docker config rm`
* `docker secret create` / `docker secret ls` / `docker secret rm`

---

### 🔹 8. **Plugins**

* `docker plugin install` / `docker plugin ls` / `docker plugin rm` / `docker plugin enable` / `docker plugin disable`

---

### 🔹 9. **Checkpoint & restore** (experimental)

* `docker checkpoint create`
* `docker start --checkpoint`

---

### 🔹 10. **Outros pontos da doc**

Além dos comandos, a documentação oficial cobre:

* **Storage drivers** (`overlay2`, `btrfs`, `zfs`, etc.).
* **Logging drivers** (`json-file`, `syslog`, `journald`, etc.).
* **Daemon (`dockerd`)**

  * Configuração via flags (`--debug`, `--storage-driver`)
  * Configuração via `daemon.json`.
* **Rootless mode** – rodar Docker sem privilégios root.
* **API do Docker Engine** – REST API para automação.
* **Compose plugin** (`docker compose` já integrado no CLI novo).

---

# 🐳 **PASSO A PASSO DOCKER COM DESCRIÇÕES**

```bash
# 1. Executa container Ubuntu interativo com porta 8080
docker container run -it -p 8080:8080 ubuntu /bin/bash

# Usar names para facilitar
docker run --name meu-container -it -p 8080:8080 ubuntu

# 2. Lista containers em execução
docker ps 

# 3. Lista todos os containers (incluindo parados)
docker ps -a  

# Ver logs da aplicação
docker logs nome-container

# 4. Copia arquivos do diretório atual para /app no container
docker container cp . IdouNomeContainer:/app

# 5. Cria nova imagem a partir do container modificado
docker commit 2eb1e70d85b4 imagem-node  

# 6. Lista imagens disponíveis (formato novo)
docker image ls     

# 7. Lista imagens disponíveis (formato clássico)
docker images  

# 8. Remove container forçadamente pelo ID
docker rm -f 2eb1e70d85b4        

# 9. Executa nova imagem em modo interativo
docker container run -it -p 8080:8080 imagem-node /bin/bash

# 10. Executa aplicação Node.js em segundo plano
docker container run -d -p 8080:8080 imagem-node node /app/server.js

# Executar comandos dentro do container
docker exec -it nome-container bash

# 11. Lista todos os containers novamente
docker ps -a

# 12. Lista containers em execução
docker ps

# Parar todos os containers
docker stop $(docker ps -q)

# Remover todos os containers parados
docker container prune

# 13. Remove container forçadamente (precisa especificar ID)
docker rm -f

# 14. Remove outro container forçadamente (precisa especificar ID)
docker rm -f

# 15. Verifica containers existentes
docker ps -a

# 16. Verifica containers em execução
docker ps 

# 17. Lista todas as imagens disponíveis
docker image ls
```

# 🐳 **FLUXO COMPLETO DOCKER - DESENVOLVIMENTO À PRODUÇÃO**

## 🚀 **FLUXO INTEGRADO PASSO A PASSO**

```bash
# 1. 👷‍♂️ PREPARAÇÃO DO AMBIENTE
docker network create app-network

# 2. 🛠️ DESENVOLVIMENTO (Container interativo)
docker run -it -p 8080:8080 -v $(pwd):/app --name dev-container --network app-network ubuntu:22.04 /bin/bash

# → Dentro do container:
apt update && apt install -y nodejs npm curl
npm install
exit

# 3. 💾 SALVAR ESTADO DE DESENVOLVIMENTO
docker commit --author "Dev <dev@email.com>" --message "Ambiente dev configurado" dev-container app-dev:1.0

# 4. 🧹 LIMPAR CONTAINER TEMPORÁRIO
docker stop dev-container
docker rm dev-container

# 5. 🧪 TESTAR IMAGEM DEV
docker run -d -p 8080:8080 --name test-container --network app-network app-dev:1.0 npm start

# 6. 🔍 MONITORAR TESTE
docker logs -f test-container
docker stats test-container

# 7. ✅ SE TUDO OK, PREPARAR PARA PRODUÇÃO
docker exec -it test-container npm run build
docker commit test-container app-prod:1.0

# 8. 🏷️ TAGGEAR PARA REGISTRY
docker tag app-prod:1.0 meuregistro.com/app-prod:1.0

# 9. 🚀 FAZER PUSH
docker push meuregistro.com/app-prod:1.0

# 10. 🧹 LIMPAR AMBIENTE DE TESTE
docker stop test-container
docker rm test-container

# 11. 🐳 IMPLANTAR EM PRODUÇÃO
docker run -d -p 8080:8080 --name production-container --network app-network -e NODE_ENV=production meuregistro.com/app-prod:1.0

# 12. 📊 MONITORAR PRODUÇÃO
docker logs production-container
docker stats production-container
docker inspect production-container

# 13. 🔧 COMANDOS DE MANUTENÇÃO
# Ver saúde da aplicação
docker inspect --format='{{.State.Health.Status}}' production-container

# Backup de dados
docker cp production-container:/app/data ./backup/

# Acessar container para troubleshooting
docker exec -it production-container bash

# 14. 📦 ROTINA DE LIMPEZA
docker system df
docker image prune -a
docker container prune
docker network prune

# 15. 🚨 EM CASO DE PROBLEMAS
docker restart production-container
docker logs --tail 100 production-container
```

## 🔄 **FLUXO SIMPLIFICADO PARA USO DIÁRIO**

```bash
# 1. Desenvolvimento
docker run -it -v $(pwd):/app --name dev ubuntu:22.04 /bin/bash

# 2. Commit das mudanças
docker commit dev minha-app:dev

# 3. Teste
docker run -d -p 8080:8080 minha-app:dev

# 4. Deploy
docker tag minha-app:dev registry.com/app:latest
docker push registry.com/app:latest

# 5. Limpeza
docker system prune -f
```

## 📋 **COMANDOS DE VERIFICAÇÃO DO FLUXO**

```bash
# Verificar rede
docker network ls

# Verificar containers
docker ps -a

# Verificar imagens
docker images

# Verificar registry
docker image ls | grep registry.com

# Verificar logs da aplicação
docker logs --tail 50 production-container

# Verificar saúde
docker inspect --format='{{.State.Status}}' production-container
```

## ⚠️ **COMANDOS DE EMERGÊNCIA**

```bash
# Parar tudo
docker stop $(docker ps -q)

# Remover tudo
docker rm $(docker ps -aq)
docker rmi $(docker images -q)

# Limpar completamente
docker system prune -a --volumes --force
```

**Este fluxo cobre desde o desenvolvimento até a produção com monitoramento!** 🐳🚀
