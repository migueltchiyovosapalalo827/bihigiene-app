= SPEC-001: Sistema de Gestão de Estoque
:sectnums:
:toc:

== Background

Este projeto visa criar um sistema de gestão de estoque eficiente para atender às necessidades de controle de produtos, fornecedores e movimentações de estoque. O sistema será utilizado por operadores de estoque e administradores, garantindo um controle preciso, alertas automáticos e geração de relatórios.

== Requirements

Os requisitos da aplicação foram organizados com base no método MoSCoW, para definir as prioridades.

=== Must Have (Obrigatório)
- Cadastro de produtos com nome, SKU, descrição, categoria, preço de custo e preço de venda.
- Controle de estoques com suporte para múltiplos armazéns.
- Registro de movimentações de estoque (entrada, saída e ajustes manuais).
- Alertas automáticos de baixa quantidade de estoque com base em limites configuráveis por produto.
- Controle de usuários com permissões de acesso (ex.: administrador, operador de estoque).
- Dashboard com resumo de estoque, entradas/saídas recentes e produtos críticos.
- Relatórios de movimentações e histórico de estoques por período.
- **Gestão de fornecedores**: cadastro, edição, exclusão e consulta de fornecedores, com vínculo no cadastro de produtos.

=== Should Have (Importante, mas não essencial)
- Integração com fornecedores para automação de pedidos de reposição.
- Suporte a múltiplas moedas e unidades de medida.
- Função de importação/exportação de dados em formato CSV.
- API para integração com sistemas externos.

=== Could Have (Desejável)
- Aplicativo móvel para consulta rápida de estoque e registro de movimentações.
- Suporte para códigos de barras ou QR code para busca rápida de produtos.
- Relatórios gráficos avançados para análise de tendências.

=== Won't Have (Fora do escopo inicial)
- Funcionalidades avançadas de ERP, como faturamento ou contabilidade.
- Suporte a lojas físicas ou vendas diretas ao consumidor (front-end e-commerce).

== Method

=== Arquitetura Geral

A aplicação será construída seguindo uma arquitetura de camadas, baseada no padrão **MVC** (Model-View-Controller) e **RESTful API**. Os principais componentes serão:
- **Front-end:** Construído com Metronic/Vue.js, será responsável pela interface de usuário.
- **Back-end:** Desenvolvido com Laravel (PHP), para a lógica de negócios e endpoints REST.
- **Banco de Dados:** Usará MySQL para persistência de dados.
- **Serviços de Notificação:** Alertas de baixa quantidade de estoque.
- **Relatórios:** Geração e exportação de relatórios.

==== Diagrama de Componentes

```plantuml
@startuml
rectangle "Front-end" as Frontend {
    [Login UI]
    [Cadastro de Produtos]
    [Gestão de Estoques]
    [Dashboard]
}

rectangle "Back-end" as Backend {
    [API REST]
    [Autenticação]
    [Gestão de Produtos]
    [Gestão de Estoque]
    [Gestão de Fornecedores]
    [Relatórios]
    [Notificações]
}

database "Banco de Dados" as DB {
    [Produtos]
    [Estoque]
    [Movimentações]
    [Usuários]
    [Fornecedores]
}

Frontend --> Backend : HTTP/HTTPS
Backend --> DB : Queries (SQL)
@enduml
