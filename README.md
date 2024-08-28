# Authentication Service

## Descrição

Este projeto é um serviço de autenticação construído com Spring Boot, utilizando JWT (JSON Web Tokens) para a autenticação de usuários. Ele foi projetado para servir como uma solução robusta, segura e escalável para gerenciar a autenticação em aplicações RESTful.

## Funcionalidades

- **Registro de Usuários**: Permite que novos usuários sejam registrados com credenciais seguras, utilizando `BCrypt` para criptografar as senhas antes de armazená-las.
- **Autenticação JWT**: Os usuários podem fazer login e receber um token JWT, que será utilizado para autenticar requisições subsequentes.
- **Proteção de Endpoints**: Endpoints sensíveis estão protegidos por JWT, garantindo que apenas usuários autenticados possam acessá-los.
- **Filtro de Autenticação JWT**: Um filtro customizado (`JwtAuthenticationFilter`) intercepta todas as requisições e valida os tokens JWT, configurando a autenticação no contexto de segurança do Spring.
- **Configuração Centralizada**: Parâmetros como a chave secreta JWT e o tempo de expiração do token são configuráveis através de arquivos de propriedades.

## Estrutura do Projeto

- `config/`: Contém classes de configuração, incluindo a configuração de segurança (`SecurityConfig`) e o provedor de tokens JWT (`JwtTokenProvider`).
- `controller/`: Controladores REST responsáveis por gerenciar endpoints de registro e autenticação.
- `model/`: Classes de modelo, incluindo a entidade `AppUser` que representa os usuários na aplicação.
- `repository/`: Interfaces de repositório que utilizam Spring Data JPA para interagir com o banco de dados.
- `service/`: Implementações de serviços, como `CustomUserDetailsService`, que carrega os detalhes do usuário a partir do banco de dados.
- `filter/`: Contém o filtro customizado `JwtAuthenticationFilter` que valida os tokens JWT em cada requisição.

## Configuração

### Requisitos

- Java 17 ou superior
- Spring Boot 3.3.3
- Banco de Dados PostgreSQL

### Configuração do Ambiente

1. Clone o repositório:
    ```bash
    git clone https://github.com/robinhokcond1/authentication-service.git
    cd authentication-service
    ```

2. Configure o arquivo `application.properties` ou `application.yml` com suas credenciais de banco de dados e a chave secreta JWT:
    ```properties
    spring.application.name=authentication-service
    app.jwtSecret=sLg0nIJXH5XtsuGOYpeUg+e7b69bQWxSNGBFv+S86X4=
    app.jwtExpirationInMs=3600000  
    server.port=8081

    spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
    spring.datasource.username=postgres
    spring.datasource.password=postgres
    spring.jpa.hibernate.ddl-auto=update
    spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
    ```

3. Execute o serviço:
    ```bash
    ./mvnw spring-boot:run
    ```

## Endpoints

### Registro de Usuário

- **Endpoint**: `/register`
- **Método**: `POST`
- **Corpo da Requisição**:
    ```json
    {
        "username": "novo_usuario",
        "password": "senha_secreta"
    }
    ```
- **Resposta**:
    - `200 OK` se o registro for bem-sucedido
    - `400 Bad Request` se o nome de usuário já existir

### Login

- **Endpoint**: `/login`
- **Método**: `POST`
- **Corpo da Requisição**:
    ```json
    {
        "username": "novo_usuario",
        "password": "senha_secreta"
    }
    ```
- **Resposta**:
    - `200 OK` com o token JWT
    - `401 Unauthorized` se as credenciais estiverem incorretas

## Melhores Práticas e Segurança

Este projeto foi desenvolvido seguindo as melhores práticas de segurança:

- **Criptografia de Senhas**: Todas as senhas são armazenadas usando `BCrypt`, garantindo proteção mesmo em caso de comprometimento do banco de dados.
- **Autenticação com JWT**: Tokens JWT são utilizados para autenticação, com validade configurável para mitigar riscos de uso prolongado.
- **Separação de Preocupações**: A estrutura do código garante modularidade e facilita a manutenção e expansão do sistema.
- **Validação de Input**: O sistema verifica e valida os dados de entrada, minimizando o risco de injeção e outros tipos de ataque.


