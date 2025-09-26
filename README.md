# Descarte Vivo: Seu Descarte Movimenta Fortaleza!

## 1. Título e Descrição do Projeto

O **Descarte Vivo** é uma plataforma digital projetada para aprimorar a gestão de resíduos recicláveis e orgânicos na cidade de Fortaleza. Através de um sistema de moedas verdes, a plataforma conecta a população, catadores e empresas, incentivando a separação, coleta e destinação correta dos resíduos. A solução busca fortalecer a economia circular e promover a sustentabilidade urbana.

## 2. Problema Abordado e Justificativa

O descarte inadequado de resíduos em áreas urbanas gera graves problemas ambientais e sociais, como a poluição de rios e praias, o entupimento de bueiros e a desvalorização do trabalho dos catadores. A falta de infraestrutura e informação são barreiras significativas para a adesão da população à coleta seletiva.

O Descarte Vivo justifica sua criação ao oferecer uma solução tecnológica que atende a este problema de forma direta e inovadora. Ao integrar as partes interessadas e valorizar os resíduos como recursos econômicos, a plataforma não apenas limpa a cidade, mas também gera renda e promove a inclusão social. Este projeto está alinhado com o **Objetivo de Desenvolvimento Sustentável (ODS) 11: Cidades e Comunidades Sustentáveis**, contribuindo para tornar os assentamentos humanos mais resilientes e sustentáveis.

## 3. Objetivos do Sistema

* **Implementar** uma plataforma multiplataforma, intuitiva e acessível para a gestão de descarte de resíduos.
* **Engajar** a população e os principais stakeholders (catadores e empresas) em um ecossistema de economia circular.
* **Garantir** a rastreabilidade dos pacotes de resíduos, desde a criação até a destinação final.
* **Criar** um modelo sustentável e replicável para outras cidades.

## 4. Escopo do Projeto

O projeto Descarte Vivo será desenvolvido em duas etapas principais:

* **Etapa 1 (Atual):** Foco no **planejamento e na documentação técnica**. Esta fase inclui a definição da arquitetura, modelagem do banco de dados, prototipação das interfaces e a elaboração de todos os artefatos técnicos necessários para a implementação.
* **Etapa 2 (N708):** Foco na **implementação e desenvolvimento do código**. Esta fase transformará a documentação em uma solução funcional e pronta para testes.

## 5. Visão Geral da Arquitetura

A arquitetura do Descarte Vivo é baseada no padrão de **Microserviços**. Essa abordagem modular permite que a aplicação seja dividida em componentes pequenos e independentes, que se comunicam através de APIs RESTful. Isso garante maior escalabilidade, resiliência e a capacidade de desenvolvimento em paralelo.

    ```mermaid
    graph TD
        subgraph Frontend
            A[Aplicativo Mobile]
            B[Aplicação Web]
        end

        subgraph Backend
            C[API Gateway]
            subgraph Microserviços
                D[Serviço de Usuários]
                E[Serviço de Pacotes]
                F[Serviço de Finanças]
            end
        end

        subgraph Dados
            G[Banco de Dados SQL]
        end

        subgraph Serviços Externos
            H[API de Mapas]
            I[API de Pagamentos]
        end

        A -- Requisições HTTP --> C
        B -- Requisições HTTP --> C
        C -- Comunicação Interna --> D
        C -- Comunicação Interna --> E
        C -- Comunicação Interna --> F

        D -- Acesso ao Banco --> G
        E -- Acesso ao Banco --> G
        F -- Acesso ao Banco --> G
        
        E -- Requisições Externas --> H
        F -- Requisições Externas --> I


## 6. Tecnologias Propostas
### Frontend

- **Frameworks:** React e React Native

- **Linguagem:** TypeScript

### Backend

- **Linguagem:** Node.js

- **Framework:** Express.js

### Banco de Dados

- **SGBD:** PostgreSQL

### Ferramentas

- **Versionamento:** Git e GitHub

- **Prototipação:** Figma (ou similar)

- **Contêineres:** Docker

## 7. Cronograma para a Etapa 2 (N708)
O cronograma a seguir é uma estimativa para a fase de implementação do projeto.

### Mês 1: Base e Autenticação

- **Semanas 1-2:** Configuração do ambiente e desenvolvimento do Serviço de Usuários (cadastro, login).

Semanas 3-4:** Criação das telas de autenticação e perfil do usuário.

### Mês 2: Lógica Central

- **Semanas 5-6:** Desenvolvimento do Serviço de Pacotes (criação, visualização, detalhes) e das interfaces de descarte.

- **Semanas 7-8:** Implementação da lógica de transações (compra/venda de pacotes) e das telas de mapa.

### Mês 3: Finalização e Testes

- **Semanas 9-10:** Desenvolvimento do Serviço de Finanças (compra/venda de moedas) e da loja (marketplace).

- **Semanas 11-12:** Testes de integração, refatoração de código e preparação do ambiente de produção.

## 8. Integrantes da Equipe

Amanda Freire Ferreira - 2323777 (Papel: Arquiteta de Software)


Antonia Samara Patricio Santos - 2323807 (Papel: Designer de UX/UI)

Cristiano Magno Rodrigues Dos Santos - 2323785 (Papel: Desenvolvedor Backend)

Davi Gaspar Da Cruz - 23238633 (Papel: Desenvolvedor Frontend)

Italo Bruno Castro De Oliveira - 2326218 (Papel: Analista de Negócio)

Raphaela Vidal De Oliveira - 2326911 (Papel: Gerente de Projeto)

## 9. Responsabilidades

### Gerente de Projeto

- **Planejamento:** Elaborar e monitorar o cronograma do projeto, definindo prazos para cada entrega.

- **Coordenação:** Distribuir tarefas e garantir que a equipe esteja alinhada e motivada.

- **Comunicação:** Atuar como o principal ponto de contato entre a equipe e o professor, comunicando o progresso e quaisquer desafios.

- **Gerenciamento de Riscos:** Identificar possíveis problemas (como atrasos ou falhas) e planejar soluções para eles.

### Arquiteto de Software

- **Desenho do Sistema:** Propor e documentar a arquitetura completa do software (microserviços, APIs, etc.).

- **Escolha de Tecnologias:** Selecionar as ferramentas e os frameworks mais adequados para a implementação.

- **Padrões de Design:** Garantir que a equipe siga os padrões arquiteturais definidos para manter a consistência e a qualidade do código.

- **Documentação Técnica:** Liderar a elaboração dos documentos técnicos, como a documentação de arquitetura e das APIs.

### Analista de Negócio

- **Levantamento de Requisitos:** Coletar e analisar as necessidades do projeto para traduzi-las em requisitos funcionais e não-funcionais.

- **Ponte de Comunicação:** Atuar como o elo entre a ideia do negócio e o time técnico, garantindo que o que será desenvolvido atenda aos objetivos do projeto.

- **Análise do Impacto:** Avaliar como a solução de software pode gerar o impacto social desejado, alinhando-se ao ODS 11.

- **Validação:** Ajudar a validar o produto final para ter certeza de que ele resolve o problema inicial.

### Designer de UX/UI

- **Design Centrado no Usuário:** Criar uma experiência de usuário (UX) intuitiva e agradável, pensando nos fluxos de interação da plataforma.

- **Prototipação:** Desenvolver os wireframes e protótipos de alta fidelidade para as interfaces web e mobile.

- **Design Visual (UI):** Definir a identidade visual do projeto, incluindo cores, tipografia e ícones.

- **Testes de Usabilidade:** Conduzir testes com usuários para validar o design e fazer melhorias.

### Desenvolvedor Backend

- **Lógica do Servidor:** Construir os microserviços, as APIs e a lógica de negócio do sistema.

- **Gestão de Dados:** Criar a estrutura do banco de dados e garantir que a comunicação com ele seja segura e eficiente.

- **Segurança:** Implementar a autenticação de usuários, a validação de dados e outras medidas de segurança.

- **Integração:** Conectar os serviços de terceiros, como as APIs de geolocalização e de pagamento.

### Desenvolvedor Frontend

- **Desenvolvimento da Interface:** Codificar as interfaces web e mobile, seguindo os protótipos e o design definidos.

- **Experiência do Usuário:** Garantir que a aplicação seja fluida, rápida e responsiva em diferentes dispositivos.

- **Consumo das APIs:** Integrar o frontend com o backend, fazendo as requisições corretas para obter e enviar dados.

- **Manutenção:** Resolver bugs e otimizar o desempenho das interfaces.