# Cadastro e Login com HTML/JS/PHP - Servidor

## 🧾 Resumo

Sistema de gerenciamento de vendas voltado para lojas físicas, com suporte a múltiplos terminais conectados em rede.

- **Objetivo:** Gerenciar vendas, caixas e impressão de cupons
- **Tecnologia:** Electron, Node.js, Express, Cors, OS, Dotenv, Jsonwebtoken, Bcrypt, SQLite ou MySQL
- **Estrutura:** 1 servidor (PC principal) + vários clientes conectados em rede
- **Impressão:** Térmica 48mm (ESC/POS)
- **Dispositivos:** Leitor de código de barras + Teclado

## 🚀 Tecnologias e Bibliotecas utilizadas

- Electron
- Node.js
- Express
- Cors
- OS
- Dotenv
- Jsonwebtoken
- Bcrypt
- MySQL ou SQLite (configurável)

## Como usar
1. Clone este repositório
2. Instale as dependências
3. Rode o projeto com `node main.js`, `nodemon main.js`

## LOGIN
    ROTA MÉTODO POST = /auth
    JSON {
        cpf: "00000000000",
        senha: "senha"
    }

    RETORNO:

    JSON {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MzEsImlhdCI6MTc0ODcxMzU5MiwiZXhwIjoxNzQ4NzQyMzkyfQ.IxhKIX3CX0ykSOjUzvYr-FUSw9Ycl9PxioKv2jRyY30"
    }
    ou 
    JSON {
        "erro": "Usuário não encontrado"
    }
    ou
    JSON {
        "erro": "Senha inválida"
    }

## STATUS DO SISTEMA
    ROTA MÉTODO GET = /status
    
    RETORNO:
    
    JSON {
        "status": "Online",
        "ip": "192.XXX.X.XXX",
        "port": "XXXX"
    }

## CRUD USUÁRIOS
    ROTA CADASTRO - MÉTODO POST = /users

    ENVIO:

    JSON {
        "nome": "NOME COMPLETO",
        "cpf":"XXXXXXXXXXX", 
        "cep":"XXXXXXXX", 
        "logradouro":"ENDEREÇO COMPLETO", 
        "numero":"XXXX", 
        "cargo":"CARGO", 
        "contato":"XXXXXXXXXXX", 
        "recado":"XXXXXXXXXXX", 
        "nivel":"X",
        "senha": "sehha"
    }
    
    RETORNO:
    
    JSON {
        "status": "Online",
        "ip": "192.XXX.X.XXX",
        "port": "XXXX"
    }


## Autor
- [@seuUsuarioGitHub](https://github.com/AderaldoGit/KimPOS-Server)