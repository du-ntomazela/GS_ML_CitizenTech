# 🚦 Semáforo Inteligente — Machine Learning

Previsão da lentidão do trânsito de São Paulo 30 minutos à frente, com **Random Forest** e dados reais da CET-SP, para que o Semáforo Inteligente ajuste o tempo de verde **antes** do congestionamento se formar.

Projeto da **Global Solution FIAP 2026.2 — Desafio CitizenTech**, disciplina **Inteligência Artificial & Machine Learning**.

## Integrantes

| Nome | RM |
|---|---|
| Eduardo Tomazela | RM556807 |
| Luiz Henrique Silva | RM555235 |
| Léo Masago | RM557768 |

## Ficha da CitizenTech

| Item | Resposta |
|---|---|
| Nome da CitizenTech | Semáforo Inteligente |
| Cidade | São Paulo (SP) |
| Cidadão beneficiado | quem se desloca no horário de pico e os pacientes transportados por ambulâncias |
| Problema, em uma frase | semáforos em ciclo fixo dão o mesmo verde às 7h e às 19h, gerando filas e ambulâncias presas no trânsito |
| Como funciona | cada cruzamento conta as filas e envia os números; o backend decide o tempo de verde e abre "ondas verdes" para ambulâncias |
| O que esta parte faz | prevê a lentidão dos próximos 30 minutos para a central agir antes da fila se formar |
| Indicador de impacto | erro médio de 0,90 ponto percentual na previsão, 24% menor do que supor que o trânsito continua igual |
| ODS conectados | ODS 11 (cidades sustentáveis), ODS 3 (saúde e bem-estar), ODS 9 (inovação e infraestrutura) |
| Vídeo | _link do YouTube (não listado)_ |

## Pergunta de ML e resultado

**Pergunta:** dado o horário, o dia da semana, a lentidão atual e as ocorrências registradas, qual será a lentidão do trânsito de São Paulo daqui a 30 minutos? (regressão)

| Modelo | MAE treino | MAE teste (sexta) | R² teste |
|---|---|---|---|
| Linha de base (repetir a lentidão atual) | – | 1,19 | 0,79 |
| **Random Forest** (50 árvores, profundidade 3, folha mínima 3) | 0,68 | **0,90** | **0,90** |

Detalhes, gráficos e discussão de overfitting em [RELATORIO_ML.md](RELATORIO_ML.md).

## Dados

Dados reais da **CET-SP**, publicados no UCI Machine Learning Repository: [Behavior of the urban traffic of the city of São Paulo in Brazil](https://archive.ics.uci.edu/dataset/483), de 14 a 18/12/2009, das 7h às 20h, em janelas de 30 minutos (135 registros, licença CC BY 4.0). Fonte, período e dicionário de dados em [dados/README.md](dados/README.md).

## Estrutura

| Arquivo | Conteúdo |
|---|---|
| `01_analise_exploratoria.ipynb` | qualidade dos dados, lentidão por hora e por dia, ocorrências, autocorrelação |
| `02_preparacao.ipynb` | limpeza, criação de variáveis, alvo de 30 min e divisão treino (seg–qui) / teste (sexta) |
| `03_treino_random_forest.ipynb` | linha de base, GridSearchCV com 27 combinações (GroupKFold por dia), métricas treino × teste, importância |
| `RELATORIO_ML.md` | relatório do problema à conclusão |
| `dados/` | dataset bruto, dataset preparado, treino e teste |
| `img/` | gráficos usados no relatório |
| `resultados_grid.csv` | MAE de treino e validação das 27 combinações |
| `modelo_rf_lentidao.joblib` | modelo treinado |

## Como executar (Windows / PowerShell)

```powershell
cd ml
python -m venv .venv
Set-ExecutionPolicy -Scope Process Bypass
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
jupyter notebook
```

Execute os notebooks na ordem 01 → 02 → 03 (Kernel → Restart & Run All). Os notebooks já estão salvos executados.
