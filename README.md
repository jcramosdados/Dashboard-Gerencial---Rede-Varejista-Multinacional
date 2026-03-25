# 📊 Dashboard Varejo – Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-green?style=for-the-badge)

Dashboard desenvolvido em Power BI para análise de desempenho de uma empresa varejista,
cobrindo vendas, descontos, margem, participação por categoria/produto e segurança de
dados por país (RLS dinâmico).

---

## 📁 Estrutura do repositório


📦 dashboard-varejo-powerbi ├── 📂 pbix/ │ └── dashboard_varejo.pbix ├── 📂 docs/ │ ├── manual_dashboard.pdf │ └── capa_manual.png ├── 📂 data/ │ └── dicionario_de_dados.xlsx └── README.md

---

## 🎯 Objetivo

- Monitorar vendas brutas e líquidas por período, país, loja, categoria e produto.
- Analisar descontos e seu impacto na margem.
- Acompanhar crescimento em relação ao ano anterior (LY).
- Identificar TOP 10 produtos por faturamento líquido.
- Garantir acesso seguro por país via RLS dinâmico.

---

## 📐 Modelo de dados

| Tabela                  | Tipo      | Descrição                                      |
|-------------------------|-----------|------------------------------------------------|
| `fVendas`               | Fato      | Transações de venda (qtd, preço, custo)        |
| `dCalendario`           | Dimensão  | Calendário para inteligência de tempo          |
| `dProdutos`             | Dimensão  | Cadastro de produtos                           |
| `dSubCategoriaProdutos` | Dimensão  | Subcategorias de produtos                      |
| `dCategoriaProdutos`    | Dimensão  | Categorias de produtos                         |
| `dLojas`                | Dimensão  | Cadastro de lojas                              |
| `dLocalidades`          | Dimensão  | País, estado, cidade                           |
| `dPromocoes`            | Dimensão  | Percentual de desconto por promoção            |
| `dSegurancaPais`        | Segurança | Mapeamento usuário × país para RLS             |

---

## 📊 Métricas DAX

### Financeiras

| Medida                        | Descrição                                          |
|-------------------------------|----------------------------------------------------|
| `Vendas brutas`               | Quantidade × Preço unitário                        |
| `Valor total de desconto`     | Quantidade × Preço × % desconto da promoção        |
| `Vendas líquidas`             | Vendas brutas – Desconto                           |
| `Custo total`                 | Quantidade × Custo unitário                        |
| `Margem`                      | Vendas líquidas – Custo total                      |
| `% Margem`                    | Margem ÷ Vendas líquidas                           |
| `Vendas brutas LY`            | Vendas brutas do mesmo período do ano anterior     |
| `% crescimento vs LY`         | (Vendas atuais – LY) ÷ LY                         |
| `% Desconto sobre vendas brutas` | Desconto ÷ Vendas brutas                        |

### Mix e participação

| Medida                        | Descrição                                          |
|-------------------------------|----------------------------------------------------|
| `Quantidade vendida`          | Total de unidades vendidas                         |
| `% participação por categoria`| Participação no contexto filtrado (`ALLSELECTED`)  |
| `% participação total`        | Participação sobre o total geral (`ALL`)            |
| `Ranking produtos`            | TOP 10 produtos por vendas líquidas (`RANKX`)      |

### Usabilidade

| Medida             | Descrição                                              |
|--------------------|--------------------------------------------------------|
| `Username`         | Saudação personalizada com `USERNAME()`                |
| `RelogioData_HTML` | Data e hora em tempo real via HTML + JavaScript        |

---

## 🔒 Segurança (RLS dinâmico por país)

O acesso é controlado pela tabela `dSegurancaPais`:


dSegurancaPais ├── Usuario (e-mail) └── Pais

Relacionamento: dSegurancaPais[Pais] 1:* dLocalidades[Pais]

Filtro DAX aplicado no papel de RLS:



DAX
Copiar
dSegurancaPais[Usuario] = USERNAME()




O filtro se propaga automaticamente para `dLocalidades` → `dLojas` → `fVendas`.

---

## 🚀 Como executar

1. Clone o repositório:


bash git clone https://github.com/seu-usuario/dashboard-varejo-powerbi.git

2. Abra o arquivo `pbix/dashboard_varejo.pbix` no **Power BI Desktop**.
3. Ajuste as conexões de dados conforme seu ambiente.
4. Vá em **Modeling → Manage roles** para revisar o RLS.
5. Use **View as roles** para testar a visão por país.
6. Publique no **Power BI Service** para validação com usuários finais.

---

## 👤 Autor

**Júlio César**  
Analista de Dados & BI | Pós-graduando em Data Science  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/jcramosdados)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/jcramosdados)



