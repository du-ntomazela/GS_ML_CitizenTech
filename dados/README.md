# Dados · Inteligência Artificial & Machine Learning

## Dataset principal: lentidão do trânsito em São Paulo (CET)

| Item | Detalhe |
| --- | --- |
| Nome | Behavior of the urban traffic of the city of São Paulo in Brazil |
| Origem dos dados | CET-SP (Companhia de Engenharia de Tráfego), publicado no UCI Machine Learning Repository |
| Link oficial | https://archive.ics.uci.edu/dataset/483 |
| Cópia usada | espelho no GitHub (`ivanovitchm/ne40-ia`), conferida byte a byte (MD5 `a74fc314…`) com outras duas cópias independentes |
| Período | 14/12/2009 (segunda) a 18/12/2009 (sexta), 7h00 às 20h00 |
| Granularidade | janelas de 30 minutos, 27 por dia, 135 registros |
| Licença | CC BY 4.0 (UCI) |
| Dados pessoais | nenhum |


## Arquivos

- `bruto/sp_trafego_uci_2009.csv`: arquivo original, sem alterações (separador `;`, decimal `,`).
- `sp_trafego.csv`: dataset preparado completo (125 linhas), gerado por `../02_preparacao.ipynb`.
- `treino.csv`: segunda a quinta (100 linhas). `teste.csv`: sexta (25 linhas).

## Dicionário de dados (`sp_trafego.csv`, `treino.csv`, `teste.csv`)

| Coluna | Tipo | Descrição |
| --- | --- | --- |
| `timestamp` | datetime | início da janela de 30 min (reconstruído a partir da ordem das linhas e da hora codificada) |
| `dia_semana` | texto | segunda a sexta (usado para separar treino/teste e agrupar a validação cruzada) |
| `hora_decimal` | float | horário da janela (ex.: 18,5 = 18h30) |
| `dia_semana_num` | int | segunda (0) a sexta (4) |
| `horario_pico` | 0/1 | 1 entre 7h–10h e 17h–20h |
| `lentidao_atual` | float | % de lentidão na janela atual |
| `variacao_30min` | float | variação da lentidão em relação à janela anterior |
| `total_ocorrencias` | int | soma das 16 ocorrências |
| `ocorrencias_semaforo` | int | semáforo apagado + intermitente |
| `onibus_parado` … `semaforo_intermitente` | int | contagem de cada um dos 16 tipos de ocorrência na janela |
| **`lentidao_prox_30min`** | float | **alvo de avaliação**: % de lentidão 30 min depois |
| **`variacao_prox_30min`** | float | **alvo de treino**: `lentidao_prox_30min − lentidao_atual` |

## Limitação e como ampliar

São só 5 dias úteis. É suficiente para percorrer o ciclo de ML, mas fraco para generalizar. A ampliação recomendada é a série histórica de lentidão da CET:

- **São Paulo Traffic Jams since 2001** (Kaggle, `danlessa/sao-paulo-traffic-jams-since-2001`): todos os registros de lentidão por via de 2001 a 2019, com data, hora, via, sentido e extensão em metros. https://www.kaggle.com/datasets/danlessa/sao-paulo-traffic-jams-since-2001
- Complementos possíveis: chuva por hora do **INMET** (estação Mirante de Santana) e sinistros do **Infosiga SP**, cruzando por data e hora.

O ambiente onde este dataset foi montado não tinha acesso ao Kaggle, ao INMET nem aos portais da Prefeitura; por isso a base de 2009 foi usada como ponto de partida.
