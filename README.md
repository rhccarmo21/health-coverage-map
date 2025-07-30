
# 🏥 Mapeamento da Cobertura da Saúde da Família

[![Licença MIT](https://img.shields.io/badge/Licença-MIT-green)](https://pt.wikipedia.org/wiki/Licen%C3%A7a_MIT)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/downloads/)
[![GeoPandas](https://img.shields.io/badge/GeoPandas-Geospatial_analysis-blue)](https://geopandas.org/)

## 📌 Sumário
1. [Visão Geral](#-visão-geral)
2. [Indicadores Calculados](#-indicadores-calculados)
3. [Fontes de Dados](#-fontes-de-dados)
4. [Instalação](#-instalação)
5. [Como Usar](#-como-usar)
6. [Exemplos](#-exemplos)
7. [Estrutura do Projeto](#-estrutura-do-projeto)
8. [Contribuição](#-contribuição)
9. [Licença](#-licença)
10. [Contato](#-contato)

---

## 🌐 Visão Geral

Plataforma de análise georreferenciada que mapeia:

- 🏘️ **Cobertura populacional por equipes de Saúde da Família**
- ⚠️ **Áreas com déficit de cobertura**
- 🔄 **Sobrecarga de equipes**
- 🏥 **Correlação com indicadores de saúde**

**Aplicações:**
- Alocação eficiente de recursos
- Planejamento de expansão da ESF
- Identificação de vulnerabilidades
- Monitoramento da atenção básica

---

## 📊 Indicadores Calculados

### Métricas Principais
| Indicador | Fórmula | Ideal | Interpretação |
|-----------|---------|-------|---------------|
| Razão População/Equipe | `População/Equipes` | 3.000 | Cobertura adequada |
| Índice de Cobertura | `Pop. coberta/Pop. total` | 100% | % atendimento |
| Distância Média | `Σ(distâncias)/n` | ≤5km | Acessibilidade |
| Carga de Trabalho | `Cadastros/ACS` | ≤750 | Equilíbrio de demanda |

```python
from health_coverage import calculate_coverage

metrics = calculate_coverage(
    population_data,
    health_teams,
    max_ratio=3000  # Parâmetro ajustável
)
```

---

## 📂 Fontes de Dados

| Fonte | Dados | Escala | Acesso |
|-------|-------|--------|--------|
| e-SUS AB | Cadastros da ESF | UBS | API |
| CNES | Equipes de saúde | Estabelecimento | FTP |
| IBGE | População | Setor censitário | CSV |
| DATASUS | Indicadores de saúde | Municipal | TABNET |

**Estrutura Básica:**
```python
import geopandas as gpd

gdf = gpd.read_file('ubs.shp')
gdf['cobertura'] = gdf['pop_cadastrada']/gdf['pop_total']
```

---

## ⚙️ Instalação

### Requisitos
- Python 3.9+
- PostgreSQL+PostGIS (para grandes bases)
- 4GB RAM (8GB recomendado)

### Via pip
```bash
pip install health-coverage-map
```

### Modo Desenvolvimento
```bash
git clone https://github.com/seu-usuario/health-coverage-map.git
cd health-coverage-map
pip install -e ".[geo]"
```

---

## 🚀 Como Usar

### 1. Dashboard Interativo
```bash
streamlit run app/coverage_dashboard.py
```

### 2. Análise Programática
```python
from health_coverage import CoverageAnalysis

ca = CoverageAnalysis('estado_sp')
results = ca.run_analysis(
    metrics=['cobertura', 'sobrecarga'],
    year=2023
)
```

### 3. Linha de Comando
```bash
health-map --municipio "São Paulo" --tema cobertura --output mapa.html
```

---

## 🏥 Exemplos Práticos

### Caso 1: Déficit de Cobertura
```python
from health_viz import plot_coverage_gap

plot_coverage_gap(
    city='Rio de Janeiro',
    threshold=0.7,  # Cobertura mínima esperada
    save_as='deficit_rj.png'
)
```
**Saída:**
![Mapa de Déficit](https://exemplo.com/mapa-deficit-rj.png)

### Caso 2: Análise de Sobrecarga
```python
overload_analysis = calculate_team_overload(
    teams_data,
    population_data,
    max_per_team=3000
)
```

---

## 🗂 Estrutura do Projeto

```
health-coverage-map/
├── data/
│   ├── raw/              # CNES, IBGE, SIAB
│   └── processed/        # Dados tratados
├── notebooks/
│   ├── exploratory/      # Análises iniciais
├── health_coverage/
│   ├── core/             # Cálculos de cobertura
│   ├── geo/              # Análise espacial
│   └── viz/              # Visualização
├── requirements.txt
└── README.md
```

---

## 🤝 Contribuição

1. **Sugira Novos Indicadores** via [issues](https://github.com/seu-usuario/health-coverage-map/issues)
2. **Padrões de Código**:
   ```python
   def calculate_coverage_ratio(pop: int, teams: int) -> float:
       """Calcula razão população/equipe
       
       Args:
           pop: População total
           teams: Número de equipes
           
       Returns:
           Razão de cobertura
       """
       return pop/(teams*3000)  # Padrão MS
   ```
3. **Fluxo Recomendado**:
   ```bash
   git checkout -b feature/novo-indicador
   git commit -m "Adiciona índice de vulnerabilidade"
   git push origin feature/novo-indicador
   ```

---

## 📜 Licença

```text
Copyright 2023 Mapeamento da Cobertura da Saúde da Família

Permissão é concedida para uso em gestão pública...
```

---

## 📧 Contato

**Equipe de Análise em Saúde**  
[cobertura.esf@saude.gov.br](mailto:cobertura.esf@saude.gov.br)  

**Suporte Técnico**  
[suporte.mapeamento@saude.gov.br](mailto:suporte.mapeamento@saude.gov.br)  

**Acesso ao Painel**  
[![Portal](https://img.shields.io/badge/Painel_Interativo-Acesse_Aqui-blue)](https://mapa.saude.gov.br/esf)

---

💡 **Para Gestores Municipais:**  
Baixe nosso kit de implementação:  
[📘 Guia para Expansão da ESF](docs/guia_expansao_esf.pdf)

> **Nota Técnica:** Parâmetros conforme Portaria MS nº 2.488/2011 (Política Nacional de Atenção Básica).
```

### Destaques Específicos para Saúde:
1. **Parâmetros Oficiais**: Utiliza padrões do Ministério da Saúde
2. **Integração CNES/SIAB**: Dados atualizados da atenção básica
3. **Indicadores Chave**: Razão população/equipe e % de cobertura
4. **Foco em Equidade**: Identificação de áreas vulneráveis
5. **Pronto para SUS**: Compatível com sistemas do DATASUS

### Para Implementação:
1. Conectar com bases do CNES e e-SUS AB
2. Ajustar parâmetros conforme portarias locais
3. Integrar com sistemas municipais de saúde
4. Adicionar camadas de unidades de saúde existentes
