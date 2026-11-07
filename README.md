# Planejamento curricular em Jupyter

GCC118 - Programação Matemática / UFLA / 2026/2.

Aluno: Caio Teixeira Ladeira.

O problema é organizar as disciplinas restantes para concluir o curso em menos períodos e, mantendo essa duração, distribuir melhor os créditos. Esta entrega reúne as fases 2 e 3: formulação exata, testes no CBC, construção gulosa, busca local e comparação.

## Abrir e executar

O código está inteiro em [Planejamento_Curricular.ipynb](Planejamento_Curricular.ipynb). Ele pode ser aberto no Jupyter Notebook ou JupyterLab. As células trazem explicações, funções, testes, resultados e o gráfico.

Com Python 3.12, dentro desta pasta:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m jupyterlab Planejamento_Curricular.ipynb
```

Selecione o kernel Python do ambiente e use **Restart Kernel and Run All Cells**. Se já usa Jupyter, instale `requirements.txt` no mesmo ambiente do kernel selecionado. O notebook não depende de arquivos `.py` locais.

Se estiver com o notebook aberto em outro ambiente, a instalação pode ser feita em uma célula temporária com `%pip install -r requirements.txt`. Depois, reinicie o kernel e execute as células em ordem.

Na seção **1. Parâmetros**:

- `REEXECUTAR = False` carrega as medições entregues; se não houver medições, executa os cenários.
- `REEXECUTAR = True` faz novas medições em uma pasta `resultados_novos_...`, preservando o conjunto entregue.
- `SEGUNDOS = 20` limita cada chamada ao CBC. Um cenário pode ter duas chamadas.

Mesmo carregando os resultados, executar todas as células roda os testes pequenos, confere os planos e dimensões e apresenta tabelas e gráfico. O notebook entregue também conserva as saídas de sua execução completa.

## Arquivos importantes

| Caminho | Conteúdo |
| --- | --- |
| [Planejamento_Curricular.ipynb](Planejamento_Curricular.ipynb) | Código e análise em um único notebook |
| [Relatório em PDF](relatorio/Relatorio_Planejamento_Curricular_Jupyter.pdf) | Formulação, métodos, testes e comparação |
| [Fonte do relatório](relatorio/Relatorio_Planejamento_Curricular_Jupyter.md) | Texto editável |
| `dados/computacao.csv` e `dados/veterinaria.csv` | Componentes e requisitos curriculares |
| [comparacao.csv](resultados/comparacao.csv) | Tempos, objetivos, status, gaps e dimensões das chamadas |
| [planos.json](resultados/planos.json) | Planos, ambiente, chamadas e verificações |
| [qualidade_tempo.png](resultados/qualidade_tempo.png) | Figura 1; também incorporada no notebook e no PDF |
| `resultados/logs/` | Registros originais do CBC |

## Dados e hipóteses

Computação usa a matriz 2023/1, com 47 componentes selecionados. O perfil base aprovou GAC124, GAC108 e GCC218: restam 44 componentes e 156 créditos. Veterinária usa a matriz 2022/2: 63 componentes e 282 créditos pendentes. Históricos, seleção de eletivas e limites de créditos são experimentais.

Os CSV têm código, nome, créditos, carga em unidades de 10 minutos, módulo sugerido, pré-requisitos (`pre`), correquisitos (`co`) e percentual mínimo. Pré-requisitos fortes e mínimos foram reunidos em `pre`, pois o estudo assume aprovação das disciplinas ao final do período. Um correquisito admite aprovação anterior ou matrícula simultânea; relações recíprocas impõem simultaneidade.

Em Computação, Ética exige 60% e os TCCs exigem 65% da carga total aprovada antes do período. O denominador fixo é 16.968 unidades (2.828 horas-relógio), incluindo 108 horas complementares. O histórico assume zero horas complementares aprovadas. Cada TCC tem zero créditos, mas 850 unidades de carga. Componentes do próprio período não liberam o percentual.

Oferta, horários, vagas, equivalências e reprovações futuras não são modelados. A análise sistemática de incertezas e a apresentação final são etapas posteriores.

## Interpretação dos testes

Há nove cenários e uma execução por método e cenário. Os sintéticos crescem de 8 para 16 e 24 disciplinas. Os demais variam capacidade, histórico e prazo de Computação e incluem Veterinária.

`Optimal` indica ótimo provado naquela chamada. `TimeLimit` preserva uma interrupção por tempo; um plano pode ser válido sem ser ótimo. Se F1 não prova a menor duração, F2 não é executada. A falha de uma heurística não prova inviabilidade. Os tempos são observações da máquina, sem análise estatística ou controle de carga.

O relatório corresponde ao conjunto de `resultados/`. Novas execuções podem retornar tempos, limites e incumbentes diferentes; o notebook mostra os resultados do conjunto selecionado.

## Fontes

- [Computação - SIG 313](https://sig.ufla.br/modulos/publico/matrizes_curriculares/index.php?cod_matriz_curricular=313&op=abrir).
- [Veterinária - SIG 302](https://sig.ufla.br/modulos/publico/matrizes_curriculares/index.php?cod_matriz_curricular=302&op=abrir).
- [TCC I - ementa 9785](https://sig.ufla.br/modulos/publico/matrizes_curriculares/gerar_ementa.php?cod_disciplina=9785) e [TCC II - ementa 9786](https://sig.ufla.br/modulos/publico/matrizes_curriculares/gerar_ementa.php?cod_disciplina=9786).
- Enunciado GCC118, semestre 2026/2, fornecido na disciplina.
- [Documentação de execução do JupyterLab](https://jupyterlab.readthedocs.io/en/stable/user/commands.html).

Repositório: https://github.com/caiotlad/planejamento-curricular-jupyter.
