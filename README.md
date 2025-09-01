# Cadastro, Login e Logout com HTML/JS/PHP - Servidor

## 🧾 Resumo

Sistema de cadastro, login e logout usando PHP (com PDO, hash e sessões seguras) + JavaScript puro com fetch().

- **Cadastrar:** Cadastrar Usuários
- **Login:** Fazer Login com segurança 
- **Logout:** Efetuar Logout com segurança
- **Linguagens:** HTML/CSS/JS/PHP
- **Banco de Dados:** Banco de dados MySQL (banco.sql)

## 🚀 Criando Banco de Dados:

CREATE DATABASE IF NOT EXISTS sistema_login DEFAULT CHARACTER SET utf8mb4;

USE sistema_login;

CREATE TABLE IF NOT EXISTS usuarios ( 
    id INT AUTO_INCREMENT PRIMARY KEY, 
    nome VARCHAR(100) NOT NULL, 
    email VARCHAR(150) NOT NULL UNIQUE, 
    senha VARCHAR(255) NOT NULL 
);


## 📂 Estrutura de arquivos

-/cadastro_login_HTML_JS_PHP
-  ├── index.html
-  ├── painel.html
-  └── banco.sql
-  /php
-    ├── conexao.php
-    ├── register.php
-    ├── login.php
-    └── logout.php
-  /js
-    └── script.js
-  /css
-    └── style.css

## 🔌 Conexão com banco (conexao.php):
    <?php
    $host = "localhost";
    $dbname = "sistema_login";
    $usuario = "root"; // altere se necessário
    $senha = "";

    try {
        // Criamos a conexão PDO (segura contra SQL Injection)
        $pdo = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8mb4", $usuario, $senha);
        // Aqui Define modo de erro como exceção
        $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    } catch (PDOException $e) {
        die("Erro na conexão: " . $e->getMessage());
    }

## 📝 Cadastro (register.php):
    <?php
    session_start(); //Comando para iniciar sessão
    require "conexao.php"; // import

    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
        // Limpa e valida os dados recebidos que chega via Método POST
        $nome  = trim($_POST['nome']);
        $email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
        $senha = $_POST['senha'];

        // Verifica os dados e confere se a senha cumpre os requisitos maior ou igual a 6 digitos
        if (!$nome || !$email || strlen($senha) < 6) {
            http_response_code(400);
            echo "Dados inválidos";
            exit;
        }

        // Verifica se o e-mail já está cadastrado no sistema
        $stmt = $pdo->prepare("SELECT id FROM usuarios WHERE email = ?");
        $stmt->execute([$email]);
        if ($stmt->rowCount() > 0) {
            http_response_code(409); // Conflito
            echo "E-mail já cadastrado";
            exit;
        }

        // Cria hash de segurança da senha
        $hash = password_hash($senha, PASSWORD_DEFAULT);

        // Cadastra usuário no banco
        $stmt = $pdo->prepare("INSERT INTO usuarios (nome, email, senha) VALUES (?, ?, ?)");
        $stmt->execute([$nome, $email, $hash]);

        echo "Cadastro realizado com sucesso!";
    }

## 📝 Login (login.php):
    <?php
    session_start();
    require "conexao.php";

    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
        $email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
        $senha = $_POST['senha'];

        if (!$email || !$senha) {
            http_response_code(400);
            echo "Dados inválidos";
            exit;
        }

        // Pesquisa usuário no banco de dados
        $stmt = $pdo->prepare("SELECT id, nome, senha FROM usuarios WHERE email = ?");
        $stmt->execute([$email]);
        $user = $stmt->fetch(PDO::FETCH_ASSOC);

        // Verifica senha
        if ($user && password_verify($senha, $user['senha'])) {
            // Regenera ID da sessão para evitar fixação
            session_regenerate_id(true);

            $_SESSION['user_id']   = $user['id'];
            $_SESSION['user_nome'] = $user['nome'];

            echo "Sucesso";
        } else {
            http_response_code(401); // Não autorizado
            echo "E-mail ou senha inválidos";
        }
    }

## 🚪 Logout (logout.php)
    <?php
    session_start();
    session_unset(); // limpa variáveis da sessão iniciada
    session_destroy(); // encerra e elimina sessão
    echo "Logout realizado";

## 🔒 Página protegida (painel.html)




## 🌐 Pagina inicial (index.html)

## JS - Script fetch() puro no JavaScript

## CSS - Style - Estilização da página


## Autor
- [@seuUsuarioGitHub](https://github.com/AderaldoGit/cadastroLogin_HTML_JS_PHP)
