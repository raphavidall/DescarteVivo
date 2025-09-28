# Protótipo Mobile - Descarte Vivo

Este documento descreve a **estrutura inicial** e a **modelagem de dados** do protótipo mobile.  
Ele complementa a [documentação da API](../../docs/api) e a pasta de [banco de dados](../../docs/database).

---

## Visão Geral
O aplicativo mobile tem como objetivos principais:
- Facilitar o cadastro e autenticação de usuários e lojas.  
- Permitir descartar, coletar e destinar pacotes de resíduos.  
- Oferecer compra e venda de itens na loja virtual.  
- Promover a economia circular através das moedas verdes.  
- Criar uma rede sustentável com notificações e compartilhamento.  

---

## Fluxo Inicial de Telas

1. **Login / Cadastro**
   - Login com e-mail e senha.  
   - Cadastro de pessoa física ou loja.  
   - Endpoints:  
     - `POST /api/v1/usuarios/login`  
     - `POST /api/v1/usuarios/cadastro`

2. **Dashboard / Home**
   - Lista pacotes disponíveis.  
   - Atalhos: registrar pacote, encontrar pacotes, loja, perfil.  
   - Endpoint: `GET /api/v1/pacotes?status=aguardando_destino`

3. **Meus Pacotes**
   - Gerenciar pacotes descartados, destinados ou coletados.  
   - Endpoints:  
     - `POST /api/v1/pacotes/descartar`  
     - `PUT /api/v1/pacotes/{id}/solicitar-destino`  
     - `PUT /api/v1/pacotes/{id}/confirmar-destino`  
     - `PUT /api/v1/pacotes/{id}/coletar`  
     - `PUT /api/v1/pacotes/{id}/destinar`

4. **Loja**
   - Visualizar itens, comprar e vender.  
   - Endpoints:  
     - `GET /api/v1/loja/itens`  
     - `POST /api/v1/loja/comprar/{id_item}`  
     - `POST /api/v1/loja/vender`  
     - `POST /api/v1/moedas/comprar`

5. **Perfil e Rede**
   - Dados básicos do usuário e saldo.  
   - Conexões e notificações.  
   - Endpoint: `GET /api/v1/usuarios/{id}`  

---

## Modelagem de Dados

### Usuário
```json
{
  "id": 1234,
  "nome_completo": "Nome do Usuário",
  "email": "email@exemplo.com",
  "whatsapp": "85999999999",
  "endereco": {
    "rua": "Rua X",
    "numero": 10,
    "bairro": "Centro",
    "cidade": "Fortaleza",
    "estado": "CE"
  },
  "saldo_moedas": 100.00,
  "tipo": "usuario" | "loja"
}

Pacote: 
{
  "id": 101,
  "titulo_pacote": "Saco de Retalhos",
  "descricao_pacote": "Tecidos reaproveitáveis",
  "id_material": 1,
  "peso_kg": 3.0,
  "valor_pacote_moedas": 15.0,
  "valor_coleta_moedas": 5.0,
  "status": "aguardando_destino",
  "id_ponto_descarte": 1234,
  "id_ponto_destino": null,
  "id_ponto_coleta": null,
  "codigo": "TOJWMSNA",
  "data_criacao": "2025-09-28T12:30:00Z",
  "data_coleta": null,
  "data_destino": null
}

Item de loja:
{
  "id": 1,
  "nome_item": "Cupom de 15% na conta de luz",
  "descricao": "Cupom aplicável na conta de energia da Enel",
  "valor_moedas": 100,
  "tipo_item": "cupom",
  "disponibilidade": 10,
  "id_vendedor": 4567
}

Transação: 
{
  "id": 55,
  "id_origem": 1234,
  "id_destino": 4567,
  "valor": 50,
  "tipo": "compra_loja",
  "id_referencia": 1,
  "data_transacao": "2025-09-28T12:30:00Z"
}
