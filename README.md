# Sistema de Ordem de Serviço para Oficina Mecânica 🛠️🚗

Este projeto propõe um **sistema de controle e gerenciamento de ordens de serviço (OS)** para uma oficina mecânica. O objetivo é organizar e automatizar o processo de atendimento ao cliente, avaliação de veículos, execução de serviços e cálculo dos custos envolvidos.

## 🧾 Descrição do Sistema

Clientes levam seus veículos até a oficina para **consertos ou revisões periódicas**. Cada veículo é cadastrado e vinculado a um cliente, que pode ser pessoa física ou jurídica.

Após o recebimento do veículo, ele é **atribuído a uma equipe de mecânicos**, que realiza uma **avaliação técnica** e preenche uma **ordem de serviço (OS)** com a previsão da entrega e os serviços a serem realizados.

Cada OS inclui:
- Número identificador
- Data de emissão
- Data prevista para conclusão
- Valor total da OS
- Status da OS (ex: Em andamento, Finalizada, Cancelada)
- Tipos de serviços executados
- Lista de peças utilizadas
- Quantidade de mão de obra e peças aplicadas

O valor total da OS é calculado com base:
- Em uma tabela de referência de **mão de obra** (com tipo e valor unitário)
- Nas **peças aplicadas**, considerando o valor unitário e a quantidade utilizada

O cliente precisa **autorizar a execução dos serviços** antes que o trabalho seja iniciado.

A **mesma equipe** que realiza a avaliação também fica responsável por executar os serviços descritos na OS.

Os **mecânicos** são cadastrados com código, nome, endereço e especialidade, e são organizados em **equipes**, que podem atuar em múltiplas ordens de serviço.

## 🔁 Relacionamentos e Regras do Modelo

- Uma **ordem de serviço** pode conter vários serviços e várias peças.
- Um **mesmo serviço ou peça** pode ser utilizado em mais de uma ordem de serviço.
- Cada equipe pode atender diversas OS, e cada OS pode envolver mais de uma equipe.
- Há controle de quantidade de peças e horas de trabalho aplicadas por OS.

## 📌 Detalhes Adicionais Presentes no Diagrama

Além da narrativa apresentada acima, o **modelo lógico do banco de dados** (ERD) traz algumas **funcionalidades adicionais que não estavam descritas inicialmente**, como:

- **Pedido**: Entidade que representa o pedido de serviço inicial do cliente, anterior à criação da ordem de serviço. Contém a avaliação, a autorização do cliente e a data do pedido.
- **Avaliação do veículo**: É feita pela equipe de mecânicos e registrada antes da OS, vinculando o veículo e a equipe responsável.
- **Entidade `CadastroPessoas`**: Utilizada como base para herança entre pessoas físicas e jurídicas, otimizando o cadastro de clientes.
- **Tabelas associativas** para controle de:
  - Mão de obra utilizada em cada OS
  - Peças utilizadas em cada OS
  - Equipes que atuaram em cada OS
