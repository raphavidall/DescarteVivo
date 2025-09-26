# Documentação das APIs do Descarte Vivo

Este documento descreve as APIs RESTful da plataforma Descarte Vivo, organizadas por microsserviço. As APIs servem como a ponte de comunicação entre o frontend (web e mobile) e o backend do sistema, permitindo a gestão de usuários, o ciclo de vida dos pacotes de resíduos e o sistema de recompensas.

---

## 1. Serviço de Usuários e Autenticação

Este serviço gerencia o cadastro, login e perfis de todos os usuários do sistema.

### `POST /api/v1/usuarios/cadastro`
- **Função:** Cadastra um novo usuário ou loja no sistema com seus papéis.
- **Requisição (Exemplo de JSON - Usuário Comum):**
  ```json
  {
    "nome_completo": "Nome Completo do Usuário",
    "cpf": 00000000000,
    "email": "email@exemplo.com",
    "senha": "senhaSegura123",
    "whatsapp": "85999999999",
    "endereco": {
        "rua": "Rua Tenente João Albano",
        "numero": 00,
        "bairro": "Aerolandia",
        "cidade": "Fortaleza",
        "estado": "Ceará",
        "ponto_de_referencia": "Padaria Nova"
    }
  }

- **Requisição (Exemplo de JSON - Loja):**
  ```json
  {
    "razao_social": "Ecoponto Jangururru",
    "cnpj": 00000000000000,
    "email": "ecoponto@exemplo.com",
    "senha": "senhaSegura123",
    "whatsapp": "85999999999",
    "endereco": {
        "rua": "Rua 42",
        "numero": 100,
        "bairro": "Jangurussu",
        "cidade": "Fortaleza",
        "estado": "Ceará",
        "ponto_de_referencia": "Pastelaria da Esquina"
    }
  }

- **Resposta de Sucesso (201 Created):**
  ```json
  {
    "nome_completo": "Nome Completo do Usuário",
    "email": "email@exemplo.com",
    "saldo_moedas": 0
  }

- **Resposta de Erro (400 Bad Request):**
  ```json
  {
    "erro": "E-mail já cadastrado."
  }

### `POST /api/v1/usuarios/login`
- **Função:** Autentica um usuário e retorna um token de acesso JWT.
- **Requisição (Exemplo de JSON):**
  ```json
  {
    "email": "email@exemplo.com",
    "senha": "senhaSegura123"
  }

- **Resposta de Sucesso (200 OK):**
  ```json
  {
  "token": "seuTokenDeAcessoJWT"
  }

### `GET /api/v1/usuarios/{id}`

- **Função:** Retorna os dados básicos e o saldo de moedas de um usuário específico.

- **Parâmetros de URL:** `id` (integer, obrigatório)

- **Resposta de Sucesso (200 OK):**
  ```json
  {
    "nome_completo": "Nome Completo do Usuário",
    "email": "email@exemplo.com",
    "saldo_moedas": 50.75
  }


## 2. Serviço de Pacotes e Logística

Este serviço gerencia o ciclo de vida dos pacotes de resíduos.

### `POST /api/v1/pacotes/descartar`

- **Função:** Cria um novo pacote de resíduos.

- **Requisição (Exemplo de JSON):**
  ```json
  {
    "título_pacote": "Pacote de Tecidos",
    "descricao_pacote": "Uma breve descrição opcional.",
    "id_material": 1, 
    "peso_kg": 5.2
  }

- **Resposta de Sucesso (201 Created):**
  ```json
  {
    "id": 101,
    "status": "pendente_destino",
    "id_ponto_descarte": 1234, // id do usuário que está descartando
    "id_material": 1, 
    "peso_kg": 5.2,
    "valor_pacote_moedas": 15.00
  }

### `PUT /api/v1/pacotes/{id}/solicitar-destino`

- **Função:** Um usuário solicita a destinacao de um pacote.
- **Parâmetros de URL:** `id` (integer, obrigatório)

- **Requisição (Exemplo de JSON):**
  ```json
  {
    "id_ponto_destino": 2345 // id do usuário que está solicitando a destinação
  }

- **Resposta de Sucesso (201 Created):**
  ```json
  {
    "mensagem": "Destinacao solicitada com sucesso.",
    "status": "aguardando_confirmacao"
  }

### `PUT /api/v1/pacotes/{id}/confirmar-destino`

- **Função:** Um usuário aprova a destinacao de um pacote criado por ele.
- **Parâmetros de URL:** `id` (integer, obrigatório)

- **Resposta de Sucesso (201 Created):**
  ```json
  {
    "mensagem": "Destinacao aprovada com sucesso.",
    "id": 101,
    "id_ponto_descarte": 1234, // id do usuário descartou
    "id_ponto_destino": 2345,
    "id_material": 1, 
    "peso_kg": 5.2,
    "valor_pacote_moedas": 15.00,
    "codigo": "TOJWMSNA", // qr code de transação do pacote
    "status": "aguardando_coleta"
  }

### `PUT /api/v1/pacotes/{id}/coletar`

- **Função:** Um usuário registra a coleta de um pacote.
- **Parâmetros de URL:** `id` (integer, obrigatório)

- **Requisição (Exemplo de JSON):**
  ```json
  {
    "codigo": "TOJWMSNA" // qr code de transação do pacote
  }

// Se o ponto de coleta for o mesmo ponto de destino
- **Resposta de Sucesso (201 Created):**
  ```json
  {
    "mensagem": "Pacote destinado com sucesso.",
    "id": 101,
    "id_ponto_descarte": 1234, // id do usuário descartou
    "id_ponto_destino": 2345,
    "id_ponto_coleta": 2345,
    "id_material": 1, 
    "peso_kg": 5.2,
    "valor_pacote_moedas": 15.00,
    "status": "finalizado"
  }

// Se o ponto de coleta for diferente do ponto de destino
- **Resposta de Sucesso (201 Created):**
  ```json
  {
    "mensagem": "Pacote coletado com sucesso.",
    "codigo": "TOJWMSNA",
    "status": "em_transporte"
  }

### `PUT /api/v1/pacotes/{id}/solicitar-coleta`

- **Função:** Um usuário solicita a terceirização da coleta de um pacote.
- **Parâmetros de URL:** `id` (integer, obrigatório)

- **Resposta de Sucesso (201 Created):**
  ```json
  {
    "mensagem": "Coleta solicitada com sucesso.",
    "status": "aguardando_coleta"
  }


### `PUT /api/v1/pacotes/{id}/destinar`

- **Função:** Um usuário registra o destino de um pacote.
- **Parâmetros de URL:** `id` (integer, obrigatório)

- **Requisição (Exemplo de JSON):**
  ```json
  {
    "codigo": "TOJWMSNA" // qr code de transação do pacote
  }

// Se o ponto de coleta for o mesmo ponto de destino
- **Resposta de Sucesso (201 Created):**
  ```json
  {
    "mensagem": "Pacote destinado com sucesso.",
    "id": 101,
    "id_ponto_descarte": 1234,
    "id_ponto_destino": 2345,
    "id_ponto_coleta": 3456,
    "id_material": 1, 
    "peso_kg": 5.2,
    "valor_pacote_moedas": 15.00,
    "valor_coleta_moedas": 5.00,
    "status": "finalizado"
  }

### `GET /api/v1/pacotes?status=aguardando_destino`

- **Função:** Lista os pacotes disponíveis para serem comprados e/ou coletados.
- **Parâmetros de URL:** `status` (string, obrigatório)
- **Resposta de Sucesso (200 OK):** Retorna uma lista de pacotes disponíveis para destino.
    ```json
  [
    {
        "id": 101,
        "id_ponto_descarte": 1234,
        "id_material": 1, 
        "peso_kg": 5.2,
        "valor_pacote_moedas": 15.00,
        "status": "aguardando_destino"
    },
    {
        "id": 102,
        "id_ponto_descarte": 1234,
        "id_material": 3, 
        "peso_kg": 2.4,
        "valor_pacote_moedas": 8.00,
        "status": "aguardando_destino"
    }
  ]

## 3. Serviço de Finanças e Loja

Este serviço gerencia a compra e venda de moedas verdes e o marketplace.

### `POST /api/v1/moedas/comprar`

- **Função:** Permite que um usuário compre moedas verdes com dinheiro real. Dispara um crédito na conta do usuário.

- **Requisição (Exemplo de JSON):**
    ```JSON
    {
    "id_usuario": 1234,
    "valor_reais": 50.00
    }

- **Resposta de Sucesso (200 OK):**
    ```JSON
    {
    "mensagem": "Compra realizada com sucesso.",
    "moedas_adicionadas": 100
    }

### `GET /api/v1/loja/itens`

- **Função:** Lista todos os itens disponíveis na loja.

- **Resposta de Sucesso (200 OK):**
    ```JSON
    [
        { "id": 1, 
        "nome_item": "Cupom de 15% na conta de luz",
        "valor_moedas": 100 
        }
    ]

### `POST /api/v1/loja/vender`

- **Função:** Um usuário vende um produto/serviço na loja. Dispara um crédito na conta do vendedor quando o item é comprado.

- **Requisição (Exemplo de JSON):**
    ```JSON
    {
        "id_vendedor": 4567,
        "nome_item": "Serviço de consultoria ambiental",
        "valor_moedas": 500
    }

- **Resposta de Sucesso (201 Created):**
    ```JSON
    {
        "id_item": 3,
        "mensagem": "Item adicionado à loja com sucesso."
    }

### `POST /api/v1/loja/comprar/{id_item}`

- **Função:** Permite que um usuário compre um item da loja. Dispara um débito na conta do comprador e um crédito na conta do vendedor.

- **Parâmetros de URL:** id_item (integer, obrigatório)

- **Requisição (Exemplo de JSON):**
    ```JSON
    {
    "id_usuario": 1
    }

- **Resposta de Sucesso (200 OK):**
    ```JSON
    {
        "mensagem": "Compra realizada com sucesso.",
        "id_transacao": 55,
        "novo_saldo": 23.50
    }

- **Resposta de Erro (400 Bad Request):**
    ```JSON
    {
        "erro": "Saldo insuficiente de moedas."
    }