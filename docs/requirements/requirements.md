Documento de Requisitos e Regras de Negócio

Este documento detalha os requisitos funcionais, não-funcionais, regras de negócio, perfis de usuário e casos de uso do projeto "Descarte Vivo", servindo como a base para o desenvolvimento da plataforma.

## 1. Perfis de Usuários

A plataforma foi projetada para um único tipo de usuário, que pode assumir múltiplos papéis de acordo com suas ações na plataforma.

- **Usuário Geral:** Qualquer pessoa ou entidade (física ou jurídica) que se cadastra na plataforma. Este perfil genérico pode assumir os seguintes papéis:

- **Ponto de Descarte:** Cria pacotes de resíduos e os disponibiliza para destinação.

- **Ponto de Coleta:** Transporta pacotes de resíduos do ponto de descarte para o ponto de destino.

- **Ponto de Destino:** Adquire pacotes de resíduos e os destina de forma adequada.

- **Vendedor da Loja:** Cadastra e vende produtos ou serviços na loja da plataforma.

## 2. Requisitos Funcionais (RF)

Estes requisitos descrevem o que o sistema deve fazer.

### RF01: Gerenciamento de Usuários:

- **RF01.1:** O sistema deve permitir o cadastro de novos usuários com e-mail, senha, nome completo, tipo de documento (CPF/CNPJ) e endereço.

- **RF01.2:** O sistema deve permitir o login e logout de usuários.

- **RF01.3:** O sistema deve permitir que o usuário visualize e edite seus dados de perfil e saldo de moedas verdes.

- **RF01.4:** O sistema deve permitir a redefinição de senha via e-mail.

### RF02: Gerenciamento de Pacotes de Resíduos:

- **RF02.1:** O sistema deve permitir que um usuário "Ponto de Descarte" crie um novo pacote, especificando o tipo de material, peso, localização e valor em moedas verdes.

- **RF02.2:** O sistema deve exibir pacotes disponíveis em forma de lista ou mapa, permitindo a visualização por localização, tipo de material e status.

- **RF02.3:** O sistema deve permitir que um "Ponto de Destino" adquira um pacote disponível.

- **RF02.4:** O sistema deve permitir que um "Ponto de Coleta" confirme a coleta de um pacote.

- **RF02.5:** O sistema deve permitir que o "Ponto de Destino" confirme o recebimento de um pacote.

- **RF02.6:** O sistema deve permitir a troca de mensagens entre os envolvidos na transação de um pacote (descarte, coleta, destino).

### RF03: Sistema de Transações Financeiras (Moedas Verdes):

- **RF03.1:** O sistema deve processar a aquisição de um pacote, debitando moedas do "Ponto de Destino" e creditando-as no "Ponto de Descarte".

- **RF03.2:** O sistema deve processar o pagamento da coleta, debitando moedas do "Ponto de Destino" e creditando-as no "Ponto de Coleta".

- **RF03.3:** O sistema deve permitir que usuários comprem moedas verdes com dinheiro real.

### RF04: Gerenciamento da Loja:

- **RF04.1:** O sistema deve permitir que usuários vendam produtos ou serviços na loja em troca de moedas verdes.

- **RF04.2:** O sistema deve permitir que usuários comprem produtos ou serviços da loja.

- **RF04.3:** O sistema deve exibir o catálogo de produtos/serviços da loja com seus respectivos valores em moedas verdes.

## 3. Requisitos Não-Funcionais (RNF)

Estes requisitos descrevem como o sistema deve funcionar, não o que ele deve fazer.

- **RNF01:** Usabilidade: A interface deve ser intuitiva e fácil de usar, tanto em dispositivos móveis quanto em navegadores de desktop.

- **RNF02:** Desempenho: O sistema deve processar solicitações de API em no máximo 500ms.

- **RNF03:** Escalabilidade: A arquitetura deve ser escalável para suportar o crescimento futuro da base de usuários e o volume de transações.

- **RNF04:** Segurança: O sistema deve proteger os dados dos usuários com criptografia e garantir a segurança das transações de moedas verdes.

- **RNF05:** Acessibilidade: A plataforma deve considerar as diretrizes de acessibilidade para garantir uma experiência adequada a diferentes tipos de usuários.

## 4. Regras de Negócio

Estas são as regras internas que regem o comportamento da plataforma.

- **RN01:** Um usuário não pode atuar como "Ponto de Coleta" para um pacote que ele mesmo criou como "Ponto de Descarte".

- **RN02**: O valor em moedas verdes de um pacote é definido pelo sistema com base no peso e tipo do material.

- **RN03:** O valor em moedas verdes da coleta é definido pelo sistema com base na distância entre o Ponto de Descarte e o Ponto de Destino.

- **RN04:** Transações de moedas verdes só podem ser concluídas após a confirmação das etapas logísticas pelos usuários envolvidos.

- **RN05:** O valor de um pacote ou serviço na loja não pode ser negativo.

- **RN06:** O saldo de moedas verdes de um usuário não pode ser negativo.

- **RN07:**Um pacote não pode ter mais de um Ponto de Coleta ou Destino.

## 5. Casos de Uso

A seguir, exemplos de como os usuários interagem com o sistema.

### CU01: Criar um Novo Pacote de Resíduos

- **Ator:** Usuário Geral (com papel "Ponto de Descarte").

- **Fluxo:** O usuário acessa a tela de criação de pacote, preenche os dados do material e do valor, e o sistema exibe o pacote no mapa como "disponível".

### CU02: Adquirir e Pagar por um Pacote

- **Ator:** Usuário Geral (com papel "Ponto de Destino").

- **Fluxo:** O usuário localiza um pacote no mapa, clica em "adquirir", e a plataforma debita o valor do pacote e da coleta de seu saldo e credita o valor ao Ponto de Descarte. O status do pacote muda para "em transporte".

### CU03: Coletar e Entregar um Pacote

- **Ator:** Usuário Geral (com papel "Ponto de Coleta").

- **Fluxo:** O usuário localiza um pacote em transporte, se desloca até o Ponto de Descarte e confirma a coleta via aplicativo. Em seguida, ele se desloca ao Ponto de Destino, que confirma o recebimento. A plataforma credita o valor da coleta ao usuário.