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
