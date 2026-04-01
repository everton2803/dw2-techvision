# TechVision - Blog e Documentação Interna

Este projeto implementa uma solução completa para hospedar o blog público e a documentação interna da TechVision usando Nginx em um container Docker com virtual hosts.

## Como Funciona

### Virtual Hosts
O projeto utiliza dois **virtual hosts** (hosts virtuais) no Nginx para servir dois sites distintos a partir do mesmo servidor:
- `blog.techvision.local` → Serve o conteúdo do blog público
- `docs.techvision.local` → Serve a documentação interna da equipe

### Arquitetura
- **Nginx**: Servidor web leve e eficiente que roteia as requisições baseadas no domínio solicitado
- **Docker**: Containerização para isolamento e portabilidade
- **Docker Compose**: Orquestração simplificada do ambiente

### Estrutura de Diretórios
```
dw2-techvision/
├── blog/                   # Conteúdo do blog
│   ├── index.html          # Página principal do blog
│   └── style.css           # Estilos CSS do blog
├── docs/                   # Documentação interna
│   ├── index.html          # Página principal da documentação
│   └── style.css           # Estilos CSS da documentação
├── nginx.conf              # Configuração do Nginx com virtual hosts
├── docker-compose.yml      # Configuração do Docker Compose
└── README.md               # Este arquivo
```

## Pré-requisitos

- Docker instalado e em execução
- Docker Compose instalado
- Permissões de administrador (para editar o arquivo hosts)

## Como Executar

### 1. Configurar Hosts Locais

Para que os domínios virtuais funcionem localmente, você precisa adicionar entradas no arquivo de hosts do sistema:

**Windows:**
- Abra o Bloco de Notas como **Administrador**
- Abra o arquivo `C:\Windows\System32\drivers\etc\hosts`
- Adicione no final do arquivo:
  ```
  127.0.0.1 blog.techvision.local
  127.0.0.1 docs.techvision.local
  ```
- Salve o arquivo

**Linux/Mac:**
- Abra o terminal
- Execute: `sudo nano /etc/hosts`
- Adicione no final:
  ```
  127.0.0.1 blog.techvision.local
  127.0.0.1 docs.techvision.local
  ```
- Salve e saia (Ctrl+X, Y, Enter)

### 2. Iniciar o Servidor

No diretório raiz do projeto, execute:
```bash
docker-compose up -d
```

Este comando irá:
- Baixar a imagem do Nginx (se necessário)
- Criar e iniciar o container
- Mapear a porta 80 do container para a porta 80 do host
- Montar os volumes com os arquivos locais

### 3. Verificar o Funcionamento

**Via navegador:**
- Acesse http://blog.techvision.local
- Acesse http://docs.techvision.local

**Via linha de comando:**
```bash
# Testar blog
curl -H "Host: blog.techvision.local" http://localhost

# Testar documentação
curl -H "Host: docs.techvision.local" http://localhost
```

### 4. Parar o Servidor

Para parar o container:
```bash
docker-compose down
```

## Desenvolvimento

### Modificar Conteúdo
- Edite os arquivos em `blog/` para alterar o blog
- Edite os arquivos em `docs/` para alterar a documentação
- As mudanças são refletidas automaticamente (hot reload)

### Configuração do Nginx
O arquivo `nginx.conf` contém:
- Dois blocos `server` para cada virtual host
- Configuração básica de MIME types e logs
- Roteamento para os diretórios apropriados

### Personalização
- Para adicionar mais virtual hosts, edite `nginx.conf` e adicione novos blocos `server`
- Para alterar portas, modifique `docker-compose.yml`
- Para usar HTTPS, adicione certificados SSL e configure os blocos server

## Solução de Problemas

### Porta 80 ocupada
Se a porta 80 estiver em uso por outro serviço (como IIS ou Apache), você pode:
1. Parar o serviço conflitante, ou
2. Alterar a porta no `docker-compose.yml` (ex: `"8080:80"`)

### Hosts não resolvem
- Verifique se as entradas foram adicionadas corretamente no arquivo hosts
- Reinicie o navegador ou limpe o cache DNS

### Container não inicia
- Verifique se o Docker está rodando: `docker ps`
- Veja os logs: `docker-compose logs`

## Tecnologias Utilizadas

- **Nginx**: Servidor web de alto desempenho
- **Docker**: Plataforma de containerização
- **HTML5/CSS3**: Estrutura e estilo das páginas
- **Virtual Hosts**: Múltiplos sites em um servidor

---

**TechVision Consultoria** - Soluções em Tecnologia
   ```
   curl -H "Host: blog.techvision.local" http://localhost
   curl -H "Host: docs.techvision.local" http://localhost
   ```

6. Para parar:
   ```
   docker-compose down
   ```