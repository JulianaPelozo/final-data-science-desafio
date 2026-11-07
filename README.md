# 📺 Auditoria de Privacidade em Smart TVs

> **Dos Dados à Decisão:** análise de dados e construção de dashboard
> Atividade Final Individual de Ciência de Dados do Senac (Compet), trilha **Fullstack**

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white)
![Status](https://img.shields.io/badge/status-em%20andamento-orange)

---

## 🎯 Sobre o projeto

Este projeto é uma **auditoria de privacidade fictícia** feita com registros **simulados** de uma plataforma de Smart TVs. A base cobre:

- comportamento de visualização;
- atividade do microfone;
- classificação de sons;
- tráfego de rede (telemetria);
- publicidade personalizada.

O trabalho segue o ciclo completo de análise: diagnóstico da base, limpeza, estatística descritiva, indicadores, dashboard e conclusões.

### Perguntas que a análise busca responder

1. Em quantos intervalos houve atividade simulada do microfone?
2. Como o tráfego de rede varia conforme as configurações de privacidade?
3. Quais conteúdos aparecem com maior frequência?
4. Qual é a taxa de interação com os anúncios?
5. Existem registros que merecem investigação por possíveis inconsistências de consentimento e telemetria?

> [!IMPORTANT]
> Os dados são **sintéticos** e foram criados para fins didáticos. Eles **não representam televisores reais** de nenhum fabricante e **não servem como evidência** sobre práticas de nenhuma empresa. Tráfego de rede, sozinho, **não comprova** transmissão de áudio ou de conversas. A análise separa **fatos registrados**, **hipóteses** e **limitações**.

---

## 🗂️ Estrutura do repositório

```
final-data-science-desafio/
├── dados/
│   ├── dataset_fullstack_900_smarttv_privacidade.csv   # base original
│   └── dicionario_fullstack_smarttv.csv                # dicionário de dados
├── notebooks/
│   └── 01_diagnostico.ipynb                            # Etapa 1
├── graficos/                                           # figuras exportadas
├── relatorio/                                          # relatório final
└── README.md
```

---

## 🧭 Etapas da análise

| # | Etapa | Entrega | Status |
|:-:|---|---|:-:|
| 1 | **Compreensão dos dados**: volume, tipos, ausentes, duplicatas, inconsistências | Diagnóstico inicial | 🟡 |
| 2 | **Limpeza e transformação**: padronização, tratamento justificado, novas variáveis | Dataset tratado + log de procedimentos | ⚪ |
| 3 | **Estatística descritiva**: média, mediana, moda, dispersão, quartis, IQR, outliers | Tabela estatística + interpretação | ⚪ |
| 4 | **Indicadores**: no mínimo 4 KPIs com fórmula e interpretação | Tabela de indicadores | ⚪ |
| 5 | **Dashboard**: 4+ indicadores e 3+ gráficos | Painel visual | ⚪ |
| 6 | **Conclusões**: padrões, achados, recomendações e limitações | Relatório final (1 a 3 páginas) | ⚪ |

<sub>🟢 concluída · 🟡 em andamento · ⚪ não iniciada</sub>

---

## 📋 Sobre os dados

| Item | Descrição |
|---|---|
| **Unidade de observação** | Janela simulada de **10 minutos** de uso de uma TV |
| **Variáveis** | 16 colunas: identificadores, data/hora, conteúdo, microfone, som, consentimento, privacidade, tráfego, anúncios e região |
| **Problemas intencionais** | Duplicatas, ausências, grafias inconsistentes e valores fora do intervalo válido |

O significado de cada coluna e as regras de validade estão em [`dados/dicionario_fullstack_smarttv.csv`](dados/dicionario_fullstack_smarttv.csv).

---

## ⚙️ Como executar

```bash
# 1. Clonar o repositório
git clone <url-do-repositorio>
cd final-data-science-desafio

# 2. Criar e ativar o ambiente virtual
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 3. Instalar as dependências
pip install pandas numpy matplotlib seaborn jupyter openpyxl

# 4. Abrir os notebooks
jupyter notebook notebooks/
```

Execute os notebooks **em ordem numérica**. Cada um usa a saída do anterior.

---

## 🛠️ Ferramentas

- **Python 3.12**: linguagem principal
- **pandas / NumPy**: manipulação e estatística
- **Matplotlib / Seaborn**: gráficos e dashboard
- **Jupyter Notebook**: workflow documentado; substitui o KNIME, conforme a opção "evidências equivalentes" do enunciado

---

## 👩‍💻 Autoria

**Juliana Pelozo Pacheco**: atividade individual, Senac (Compet)

Distribuído sob a licença descrita em [LICENSE](LICENSE).
