
# Dicionario-de-Dados

Dicionário de dados interativo do banco de dados da **FH NET TELECOM**, provedor de internet residencial de Guarulhos/SP. O projeto documenta o schema `assinatura_telecom` (MySQL) com foco em governança de dados, seguindo práticas do DAMA-DMBOK e do COBIT.

**Projeto:** Plataforma Centralizada de Gestão de Clientes, Rede e Faturamento
**Disciplina:** SQL - Structured Query Language (UNICID, Análise e Desenvolvimento de Sistemas)
**Orientador:** Prof. Dr. Diego Carvalho
**Equipe:** Grupo 5

## Integrantes e papéis de governança

| Integrante | Papel | Responsabilidade |
|---|---|---|
| Pedro Gonçalves da Mota | Data Owner | cliente, endereco |
| Alessandro Tavares Brandão | Data Owner | plano, assinatura, caixa_atendimento |
| Júlio César Marques de Sousa | Data Owner | cobranca, pagamento |
| Tayrone Henrique do Carmo | Data Steward | cobranca, pagamento, ordem_servico |
| Rúben Tavares Nascimento | Data Steward | usuario, log_auditoria |
| Keveny Santos | Data Steward | equipamento, vinculo_equipamento, evento_conexao |

## O que o dicionário contém

- 13 tabelas e 86 colunas, com tipo, constraints e regra de negócio de cada atributo.
- Classificação de privacidade (LGPD/GDPR) por coluna, com badges: **DPS** (dado pessoal sensível), **DP** (dado pessoal) e **N/A**.
- Linhagem dos dados (origem e destino) e controle de acesso (RBAC) por perfil: Admin, Atendente e Técnico.
- Busca em tempo real por tabela ou coluna.
- Visualizador do DER em modal, com zoom por scroll, arrastar e botões Zoom +, Zoom - e Reset (Panzoom.js).
- Modo claro e escuro, e menu lateral responsivo para celular.
- Download da Especificação de Requisitos e Regras de Negócio em PDF.

## Estrutura de pastas

```text
/meu-dicionario
├── index.html
├── style.css
├── script.js
├── README.md
├── docs/
│   └── Especificacao_Requisitos_Regras_Negocio_BD.pdf
└── assets/
    └── der.png
```

Os nomes de arquivos são sensíveis a maiúsculas e minúsculas no GitHub Pages. Mantenha exatamente os nomes acima.

## Como executar localmente

Não há dependências para instalar. Abra o `index.html` no navegador. O Panzoom.js é carregado por CDN (jsDelivr), então é necessário acesso à internet.

## Como publicar no GitHub Pages

1. Crie um repositório público e envie o **conteúdo** desta pasta, com o `index.html` na raiz.
2. Acesse **Settings > Pages > Build and deployment > Source: Deploy from a branch**.
3. Selecione o branch **main**, pasta `/ (root)` e clique em **Save**.
4. Acesse `https://<usuario>.github.io/<repositorio>/` após alguns minutos.

## Como editar o conteúdo

Os dados do dicionário ficam no array `T` em `script.js`. Cada tabela tem nome, descrição, linhagem, RBAC e uma lista de colunas no formato `[atributo, descrição, tipo, constraints, privacidade (S/P/N)]`. Uma coluna pode ter linhagem e RBAC próprios como 6º e 7º itens. O HTML é gerado a partir desse array.

## Documentação de origem

| Artefato | Descrição |
|---|---|
| Especificação de Requisitos e Regras de Negócio | RF, RNF, RN, PR, entidades e matriz de rastreabilidade |
| DER | Modelo entidade-relacionamento (`assets/der.png`) |
| Script DDL (`scriptmysql.sql`) | Criação do schema `assinatura_telecom` no MySQL |

## Pendências antes da publicação

O dicionário só deve ser publicado depois de alinhar os três artefatos de origem. Os pontos principais da análise de coerência:

- Remover do DDL os resquícios do template Sakila (schema, placeholders e views).
- Corrigir `vinculo_equipamento` no DDL: PK com `AUTO_INCREMENT`, nomes `id_assinatura` e `id_equipamento`, e `id_equipamento_ativo` como coluna gerada STORED com UNIQUE (RN05). Depois, atualizar essa tabela em `script.js`.
- Incluir no DDL os CHECK, os índices e os defaults de TIMESTAMP previstos nos requisitos.
- Padronizar os ENUMs (`Admin` ou `Administrador`; `estoque` ou `em_estoque`) no DDL, no DER e no documento.
- Trocar "INT UNSIGNED" por "BIGINT UNSIGNED" no documento e no DER.
- Resolver RF05 (descrição e equipamento da OS) e atualizar versão, data e histórico de revisões (v1.1).
- Preencher a linha do professor e o sobrenome do representante na seção de validação.
- Exportar o documento de requisitos em PDF e o DER em PNG de alta resolução.

## Tecnologias

HTML5, CSS3 e JavaScript puro, com Panzoom.js 4.5.1 (CDN). Banco de dados documentado: MySQL 8 (InnoDB, utf8mb4).
