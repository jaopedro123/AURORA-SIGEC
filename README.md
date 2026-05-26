# SIGEC — Sistema Integrado de Gestão Energética da Colônia

Sistema em **Python puro** (sem bibliotecas externas) que representa o
funcionamento inteligente da infraestrutura energética da Colônia Marte,
desenvolvido na Atividade Integradora da Missão Aurora Siger.

O foco está na **lógica, organização e interpretação** dos dados.

---

## O que o sistema faz

O SIGEC reúne, em um único programa, as quatro capacidades trabalhadas na fase:

1. **Organiza os dados da colônia** usando três estruturas:
   - **Lista** → histórico cronológico dos sensores (`vento`, `energia`);
   - **Tabela chave-valor (dicionário)** → estado atual da base (`geração`, `consumo`, `reserva`, `clima`);
   - **Organização hierárquica (árvore)** → subsistemas separados em geração, armazenamento e consumo.

2. **Toma decisões automáticas** com regras booleanas (R1 a R5),
   sempre priorizando o **suporte à vida**.

3. **Analisa o uso de energia** comparando geração, consumo e reserva,
   e gera uma ação clara.

4. **Prevê a geração futura** com **regressão linear simples**
   (método dos mínimos quadrados), implementada manualmente.

Toda decisão é **determinística e auditável**: a mesma entrada produz sempre
a mesma saída.

---

## Como funciona (passo a passo)

O sistema recebe os dados (ex.: `energia = 40` e `consumo = 70`), aplica uma
regra de decisão (ex.: *se energia < 50 E consumo > 60 → modo economia*) e,
por fim, gera uma decisão objetiva como saída.

| Etapa | Função no código |
|-------|------------------|
| Aplicar regras de decisão (R1, R2) | `aplicar_regras_decisao()` |
| Priorizar cargas / suporte à vida (R3) | `priorizar_cargas()` |
| Avaliar balanço geração × consumo (R4, R5) | `avaliar_balanco()` |
| Analisar uso de energia (Quadro 3) | `analisar_uso_energia()` |
| Calcular a reta da regressão | `calcular_regressao()` |
| Prever energia para um vento futuro | `prever_energia()` |

---

## Exemplo de entrada e saída

### Regra de decisão
```
Entrada:  energia = 40, consumo = 70
Saída:    MODO ECONOMIA ATIVADO
          R3 -> MANTER ['LIFE', 'MED'] | DESLIGAR ['SCI', 'LOG']
```

### Análise de uso de energia
```
Entrada:  geração = 80, consumo = 30
Saída:    SUGESTÃO: armazenar energia excedente
```

### Previsão por regressão
```
Histórico: vento = [8, 10, 12]  |  energia = [20, 25, 30]
Reta ajustada:  E(v) = 2.5 * v + 0
Entrada:  vento = 11 m/s
Saída:    previsão ≈ 27,5 kW
```

---

## Como executar

```bash
python3 sigec.py
```

O programa imprime no terminal a organização dos dados, os cenários de análise,
as regras de decisão aplicadas e a previsão por regressão.

---

## Estrutura do projeto

```
.
├── sigec.py     # Sistema completo, organizado em funções
└── README.md    # Este arquivo
```

## Autor - João Pedro

Desenvolvido como atividade acadêmica integradora.  
Curso: **[Ciência da Computação]** — **[FIAP]**  
Período: **[2026/ 1º (semestre/fase)]**
