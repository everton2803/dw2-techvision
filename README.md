# TechVision Blog e Documentação

Este projeto configura um servidor Nginx em Docker com dois virtual hosts para o blog e documentação da TechVision.

## Estrutura
- `blog/`: Conteúdo do blog (HTML/CSS)
- `docs/`: Documentação interna (HTML/CSS)
- `nginx.conf`: Configuração do Nginx com dois server blocks
- `docker-compose.yml`: Orquestração do container

## Como executar

1. Certifique-se de que o Docker e Docker Compose estão instalados.

2. Adicione as seguintes entradas ao arquivo de hosts do sistema:
   - No Windows: Edite `C:\Windows\System32\drivers\etc\hosts` (como administrador)
   - No Linux/Mac: Edite `/etc/hosts`
   
   Adicione:
   ```
   127.0.0.1 blog.techvision.local
   127.0.0.1 docs.techvision.local
   ```

3. Execute o container:
   ```
   docker-compose up -d
   ```

4. Acesse os sites:
   - Blog: http://blog.techvision.local
   - Documentação: http://docs.techvision.local

5. Para testar via linha de comando:
   ```
   curl -H "Host: blog.techvision.local" http://localhost
   curl -H "Host: docs.techvision.local" http://localhost
   ```

6. Para parar:
   ```
   docker-compose down
   ```