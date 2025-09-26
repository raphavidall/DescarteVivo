# Modelagem do Banco de Dados

Este documento descreve a estrutura e os relacionamentos do banco de dados relacional (PostgreSQL) para a plataforma Descarte Vivo. O modelo de dados foi projetado para suportar uma economia circular, permitindo que qualquer usuário atue em múltiplos papéis logísticos e se comunique com outros participantes.

## Entidades e Atributos

A seguir, estão as principais entidades (tabelas) do sistema, seus atributos e a descrição de suas funcionalidades.

### 1. `usuarios`
Representa todos os usuários da plataforma, sejam eles pessoas físicas ou jurídicas.
- `id` (chave primária, serial): Identificador único do usuário.
- `nome_completo` (varchar): Nome completo do usuário.
- `email` (varchar, unique): Endereço de e-mail e login do usuário.
- `senha_hash` (varchar): Senha criptografada do usuário.
- `tipo_documento` (varchar): Tipo de documento (CPF ou CNPJ).
- `documento` (varchar, unique): Número do documento.
- `saldo_moedas` (numeric, default: 0.00): Saldo atual de moedas verdes.
- `data_cadastro` (timestamp): Data e hora do cadastro.
- `endereco` (jsonb): Endereço completo, incluindo rua, número, cidade, estado e CEP.

### 2. `tipos_de_material`
Cataloga os diferentes tipos de materiais recicláveis e orgânicos aceitos.
- `id` (chave primária, serial): Identificador único do tipo de material.
- `nome` (varchar, unique): Nome do material (ex: 'Plástico', 'Vidro', 'Orgânico').
- `valor_por_kg` (numeric): Valor base em moedas verdes por quilograma.

### 3. `pacotes_de_residuos`
Rastreia a criação e a logística de um pacote, desde o descarte até a destinação.
- `id` (chave primária, serial): Identificador único do pacote.
- `id_ponto_descarte` (integer, chave estrangeira): Referência ao usuário que criou o pacote.
- `id_ponto_coleta` (integer, chave estrangeira): Referência ao usuário que coletou o pacote.
- `id_ponto_destino` (integer, chave estrangeira): Referência ao usuário que recebeu o pacote.
- `status` (varchar): Situação do pacote ('disponivel', 'em_transporte', 'concluido').
- `valor_pacote_moedas` (numeric): Valor do pacote definido no momento do descarte.
- `valor_coleta_moedas` (numeric): Valor opcional para o serviço de coleta.
- `id_material` (integer, chave estrangeira): Tipo de material do pacote.
- `peso_kg` (numeric): Peso do material em quilogramas.
- `data_criacao` (timestamp): Data e hora da criação.
- `data_coleta` (timestamp, nulo): Data e hora da coleta.
- `data_destino` (timestamp, nulo): Data e hora da destinação.
- `localizacao` (jsonb): Coordenadas geográficas do pacote.

### 4. `mensagens_pacote`
Armazena as mensagens trocadas na área de transação de cada pacote.
- `id` (chave primária, serial): Identificador único da mensagem.
- `id_pacote` (integer, chave estrangeira): Referência ao pacote.
- `id_remetente` (integer, chave estrangeira): Referência ao usuário que enviou a mensagem.
- `mensagem` (text): Conteúdo da mensagem.
- `data_envio` (timestamp): Data e hora de envio.

### 5. `itens_da_loja`
Produtos ou serviços que podem ser comprados com moedas verdes.
- `id` (chave primária, serial): Identificador único do item.
- `id_vendedor` (integer, chave estrangeira): Referência ao usuário vendedor.
- `nome_item` (varchar): Nome do produto ou serviço.
- `descricao` (text): Descrição detalhada.
- `valor_moedas` (numeric): Valor em moedas verdes.
- `tipo_item` (varchar): Categoria ('produto', 'servico', 'cupom').
- `disponibilidade` (integer): Quantidade em estoque.

### 6. `transacoes_de_moedas`
Registra toda a movimentação de moedas verdes.
- `id` (chave primária, serial): Identificador único da transação.
- `id_origem` (integer, chave estrangeira): ID do usuário pagador.
- `id_destino` (integer, chave estrangeira): ID do usuário recebedor.
- `valor` (numeric): Quantidade de moedas.
- `tipo` (varchar): Tipo da transação. Exemplos: 'aquisicao', 'coleta', 'compra_loja', 'compra_reais', 'venda_loja'.
- `id_referencia` (integer, nulo): ID do pacote ou item da loja associado.
- `data_transacao` (timestamp): Data e hora da transação.

## Relacionamentos

Abaixo, um resumo dos principais relacionamentos entre as tabelas.

- `pacotes_de_residuos` **(1:N)** `mensagens_pacote`: Um pacote pode ter várias mensagens.
- `usuarios` **(1:N)** `pacotes_de_residuos`: Um usuário pode ser ponto de descarte, coleta ou destino para vários pacotes.
- `pacotes_de_residuos` **(1:1)** `tipos_de_material`: Um pacote tem um único tipo de material.
- `usuarios` **(1:N)** `mensagens_pacote`: Um usuário pode enviar várias mensagens.
- `usuarios` **(1:N)** `itens_da_loja`: Um usuário pode vender vários itens na loja.
- `usuarios` **(1:N)** `transacoes_de_moedas`: Um usuário pode realizar várias transações como origem ou destino.

![Diagrama ER](dataModelDescarteVivo.png)