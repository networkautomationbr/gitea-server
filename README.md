# Gitea Server em Docker 🚀

Tutorial simples e direto para subir um servidor Gitea usando Docker.

## 📋 Pré-requisitos

- Docker instalado
- Docker Compose instalado
- Porta 3000 (web) e 2222 (SSH) disponíveis

## 🚀 Como usar

### 1. Clone este repositório

```bash
apt install git -y
cd /opt/
git clone https://github.com/networkautomationbr/gitea-server.git
cd gitea-server
```
### 2. Instalar o Docker

```bash
cd /opt/gitea-server
chmod 777 install_dependencies.sh
./install_dependencies.sh
```

### 3. Suba o Gitea

```bash
cd /opt/gitea-server
sudo mkdir -p {data,postgres}
docker-compose up -d
```

### 4. Testes

```bash
docker compose ps                  # os dois containers devem estar "healthy/running"
docker compose logs -f gitea       # procure "Starting new Web server"
curl -I http://localhost:3000      # deve retornar 200
```

### 5. Acesse o Gitea

Abra seu navegador em: **http://IP:3000**

### 6. Configuração inicial

Na primeira vez, você verá a tela de instalação:

1. **Banco de dados**: Use SQLite3 (já vem configurado)
2. **Configurações gerais**: Mantenha o padrão
3. **Conta de administrador**: Crie seu usuário admin
4. Clique em **Instalar Gitea**

Pronto! Seu servidor Gitea está funcionando! 🎉

## 📂 Estrutura de dados

Os dados são salvos em:
- `./gitea-data` - Repositórios e dados do Gitea
- `./gitea-config` - Arquivos de configuração

**Importante**: Esses diretórios são criados automaticamente e persistem os dados mesmo após reiniciar o container.

## 🛠️ Comandos úteis

### Ver logs do Gitea
```bash
docker-compose logs -f
```

### Parar o Gitea
```bash
docker-compose down
```

### Reiniciar o Gitea
```bash
docker-compose restart
```

### Remover tudo (incluindo dados)
```bash
docker-compose down -v
rm -rf gitea-data gitea-config
```

## 🔧 Troubleshooting

### Porta 3000 já está em uso?

Edite o `docker-compose.yml` e mude a porta:
```yaml
ports:
  - "3001:3000"  # Use 3001 em vez de 3000
```

### Permissões no Linux?

Se tiver problemas de permissão, execute:
```bash
sudo chown -R 1000:1000 gitea-data gitea-config
```

## 📺 Video tutorial

Confira o tutorial completo no canal **Network Automation BR**!

## 📝 Licença

Apache 2.0 - Sinta-se livre para usar e modificar!
