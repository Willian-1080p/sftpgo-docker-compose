# SFTPGo com Docker Compose

Laboratório simples do SFTPGo Community executado com Docker Compose. O projeto disponibiliza o painel administrativo web e o serviço SFTP, com dados e configurações persistidos em volumes Docker.

## Serviços e portas

| Serviço | Endereço/porta |
| --- | --- |
| WebAdmin | `http://localhost:8080/web/admin` |
| SFTP | `localhost:2022` |

## Requisitos

- Docker Desktop ou Docker Engine
- Docker Compose v2
- WinSCP, FileZilla ou outro cliente compatível com SFTP para os testes

## Iniciar

Clone o repositório e entre na pasta:

```bash
git clone https://github.com/Willian-1080p/sftpgo-docker-compose.git
cd sftpgo-docker-compose
```

Suba o container:

```bash
docker compose up -d
```

Confira o estado:

```bash
docker compose ps
```

Veja os logs:

```bash
docker compose logs -f sftpgo
```

Depois, acesse:

```text
http://localhost:8080/web/admin
```

No primeiro acesso, crie o administrador do WebAdmin.

## Criar um usuário SFTP

No WebAdmin:

1. Abra **Usuários**.
2. Clique em **Adicionar**.
3. Defina usuário e senha.
4. Use um diretório como `/srv/sftpgo/data/teste-sftp`.
5. Habilite o usuário e selecione as permissões necessárias.

Para um primeiro teste local, use:

```text
Protocolo: SFTP
Servidor: localhost
Porta: 2022
Usuário: usuário criado no painel
Senha: senha definida no painel
```

## Persistência

O projeto utiliza dois volumes:

- `sftpgo_data`: arquivos dos usuários;
- `sftpgo_config`: banco de dados e configurações do SFTPGo.

Parar o container não exclui esses volumes:

```bash
docker compose down
```

Para remover também os volumes e apagar os dados persistidos:

```bash
docker compose down -v
```

> Atenção: o comando com `-v` remove os dados e configurações deste laboratório.

## Segurança

- Não exponha as portas `8080` e `2022` diretamente na internet.
- Use senhas fortes ou autenticação por chave SSH.
- Para acesso externo, configure firewall, HTTPS e uma solução segura de publicação.
- Restrinja as permissões de cada usuário ao mínimo necessário.

## Atualizar

```bash
docker compose pull
docker compose up -d
```

## Referências

- [Documentação do SFTPGo](https://docs.sftpgo.com/)
- [Projeto SFTPGo no GitHub](https://github.com/drakkan/sftpgo)
