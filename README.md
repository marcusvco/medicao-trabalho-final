# Trabalho Final: Medição e Experimentação em Engenharia de Software

## 1. Identificação básica

### 1.1 Título do experimento

Análise dos Indicadores Core Web Vitals na Taxa de Rejeição e na Conversão em Aplicações Front-End

### 1.2 ID / código

CWV-BC-EXP-2025-001

### 1.3 Versão do documento e histórico de revisão

- Versão atual: v1.0
- Histórico:
  - v1.0 (21/11/2025) — criação do plano inicial

### 1.4 Datas (criação, última atualização)

- Criação: 21/11/2025
- Última atualização: 21/11/2025

### 1.5 Autores (nome, área, contato)

- Marcus Vinícius Carvalho de Oliveira — Engenharia de Software — marcuscarvalhodeoliveira@gmail.com

### 1.6 Responsável principal (PI / dono do experimento)

- Marcus Vinícius Carvalho de Oliveira

### 1.7 Projeto / produto / iniciativa relacionada

- Módulo de monitoramento e análise de performance Front-End

## 2. Contexto e problema

### 2.1 Descrição do problema / oportunidade

Variações nos indicadores Core Web Vitals (LCP, INP e CLS) podem estar associadas a aumento da taxa de rejeição e redução de conversão em aplicações Front-End. Observam-se sintomas como abandono de páginas com carregamento lento (LCP alto), queda de interação em fluxos críticos quando há latência de entrada elevada (INP) e frustração do usuário por instabilidade visual (CLS), afetando etapas como landing pages, cadastro e checkout. A oportunidade é quantificar a relação entre níveis de CWV e métricas de negócio para orientar intervenções com maior impacto.

### 2.2 Contexto organizacional e técnico

Ambiente acadêmico (PUC), trabalho final individual com foco em aplicações Front-End. O experimento será conduzido sobre páginas representativas (ex.: landing, listagem, detalhe e conversão) em ambiente de teste e/ou produção controlada. Tecnologias e ferramentas previstas: coleta de CWV via biblioteca `web-vitals`/API do navegador, observabilidade com Google Analytics 4 (GA4) e/ou CrUX, análises em BigQuery/planilhas, e auditorias com Lighthouse/PageSpeed Insights. Processo: instrumentação leve no cliente, coleta contínua, segmentação por dispositivo/rede/origem de tráfego e análise estatística para identificar correlações e efeitos.

### 2.3 Trabalhos e evidências prévias (internos e externos)

- Documentação oficial e guias do Chrome/Web.dev sobre Core Web Vitals (definições, limiares e recomendações de otimização).
- Relatórios do Chrome UX Report (CrUX) indicando distribuição populacional de CWV para diferentes sites e segmentos.
- Estudos de mercado (ex.: Deloitte/Akamai) que relacionam melhorias de velocidade a ganhos de conversão e redução de abandono.
- Casos práticos de otimização Front-End (critical CSS, preconnect, lazy loading, redução de JS) com melhorias em CWV e impacto observado em métricas de engajamento.

### 2.4 Referencial teórico e empírico essencial

- Métricas: LCP (percepção de carregamento), INP (responsividade de interação) e CLS (estabilidade visual), com categorizações "Good/Needs improvement/Poor" conforme limiares recomendados.
- Hipóteses: melhor LCP e INP reduzem rejeição e aumentam conversão; menor CLS melhora satisfação e conclusão de tarefas.
- Modelagem: análise estatística (correlação, regressão logística/linear) e/ou experimentos A/B para estimar efeito causal, controlando variáveis de confusão (dispositivo, rede, página, origem, horário).
- Práticas de medição: coleta de campo (RUM) complementada por laboratório (Lighthouse) para diagnóstico de causas e priorização.

## 3. Objetivos e questões (Goal / Question / Metric)

### 3.1 Objetivo geral (Goal template)

Analisar os indicadores Core Web Vitals (LCP, INP, CLS) com o propósito de avaliar seu efeito na taxa de rejeição e na conversão, do ponto de vista de produto e engenharia, no contexto de aplicações Front-End representativas da iniciativa acadêmica (PUC), usando coleta de campo (RUM) e dados analíticos (GA4/CrUX).

### 3.2 Objetivos específicos

- O1: Medir e caracterizar a distribuição de LCP, INP e CLS por página, dispositivo e rede.
- O2: Quantificar a relação entre níveis de CWV e taxa de rejeição/conversão.
- O3: Identificar páginas, segmentos e causas prováveis que mais contribuem para piora de CWV.
- O4: Priorizar recomendações de otimização com potencial de impacto em negócio.

### 3.3 Questões de pesquisa / de negócio

- Q1: Como se distribuem LCP, INP e CLS por página/dispositivo/rede?
- Q2: Qual a variação de rejeição e conversão por categoria de CWV (Good/Needs improvement/Poor)?
- Q3: Qual o efeito estimado de melhorar LCP/INP/CLS em rejeição e conversão?
- Q4: Quais causas/recursos mais correlacionam com CWV ruim e qual a prioridade de correção?

### 3.4 Métricas associadas (GQM)

- Métricas principais: LCP (ms) — maior elemento renderizado; INP (ms) — latência de interação; CLS (adimensional) — instabilidade visual; fontes: `web-vitals`, GA4, CrUX.
- Métricas de negócio: Taxa de rejeição (%) e Taxa de conversão (%); fonte: GA4.
- Métricas de suporte/diagnóstico: TTFB (ms), peso total de JS/CSS (KB), número de requisições; fonte: Lighthouse/PageSpeed.
- Mapeamento:
  - Q1 → LCP/INP/CLS por página/dispositivo/rede.
  - Q2 → Rejeição/Conversão por bucket de CWV (Good/NI/Poor).
  - Q3 → Variação de Rejeição/Conversão vs. melhoria simulada/observada de LCP/INP/CLS (modelos de regressão/A-B).
  - Q4 → Diagnósticos Lighthouse (peso, bloqueios, imagens), correlação com CWV e ranking de ações.

### 3.5 Tabela GQM

| Objetivo                                  | Pergunta                                                                            | Métricas                                   |
| ----------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------ |
| O1: Medir distribuição de CWV             | Q1.1: Qual é a distribuição de LCP por página/dispositivo/rede?                     | LCP (ms); FCP (ms)                         |
| O1: Medir distribuição de CWV             | Q1.2: Qual é a distribuição de INP por tipo de interação e dispositivo?             | INP (ms); TBT (ms)                         |
| O1: Medir distribuição de CWV             | Q1.3: Qual é a distribuição de CLS por página e eventos visuais?                    | CLS; Speed Index (ms)                      |
| O2: Relacionar CWV com rejeição/conversão | Q2.1: Como a taxa de rejeição varia por bucket de LCP (bom/NI/ruim)?                | Taxa de rejeição (%); LCP (ms)             |
| O2: Relacionar CWV com rejeição/conversão | Q2.2: Como a taxa de conversão varia por bucket de INP?                             | Taxa de conversão (%); INP (ms)            |
| O2: Relacionar CWV com rejeição/conversão | Q2.3: Qual o efeito de CLS na taxa de conversão em páginas de checkout?             | Taxa de conversão (%); CLS                 |
| O3: Identificar páginas/segmentos/causas  | Q3.1: Quais páginas concentram maior LCP P75?                                       | LCP (ms); TTFB (ms)                        |
| O3: Identificar páginas/segmentos/causas  | Q3.2: Quais recursos (JS/CSS/imagens) estão mais correlacionados com INP/TBT altos? | JS bytes (KB); CSS bytes (KB); TBT (ms)    |
| O3: Identificar páginas/segmentos/causas  | Q3.3: Qual o impacto do número de requisições sobre LCP?                            | Número de requisições (contagem); LCP (ms) |
| O4: Priorizar recomendações de otimização | Q4.1: Quais ações (preload, lazy, compressão) reduzem LCP estimado?                 | LCP (ms); FCP (ms)                         |
| O4: Priorizar recomendações de otimização | Q4.2: Quais ações reduzem INP/TBT em interações críticas?                           | INP (ms); TBT (ms)                         |
| O4: Priorizar recomendações de otimização | Q4.3: Quais ações reduzem CLS em componentes instáveis?                             | CLS; Speed Index (ms)                      |

### 3.6 Tabela de métricas

| Métrica               | Descrição                                            | Unidade      |
| --------------------- | ---------------------------------------------------- | ------------ |
| LCP                   | Tempo até o maior elemento visível ser renderizado   | ms           |
| INP                   | Latência agregada de interação (responsividade real) | ms           |
| CLS                   | Instabilidade visual acumulada                       | adimensional |
| FCP                   | Tempo até o primeiro conteúdo ser exibido            | ms           |
| TBT                   | Tempo total bloqueado por tarefas longas             | ms           |
| Speed Index           | Rapidez percebida de aparecimento do conteúdo        | ms           |
| TTFB                  | Tempo até o primeiro byte da resposta                | ms           |
| JS bytes              | Tamanho total dos arquivos JavaScript carregados     | KB           |
| CSS bytes             | Tamanho total dos arquivos CSS carregados            | KB           |
| Número de requisições | Quantidade de requisições da página                  | contagem     |
| Taxa de rejeição      | Percentual de sessões com apenas uma visualização    | %            |
| Taxa de conversão     | Percentual de sessões que concluíram a meta definida | %            |

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo (incluído e excluído)

- Incluído: páginas landing, listagem, detalhe e fluxo de conversão (cadastro/checkout); instrumentação de Front-End; análise GA4/CrUX; auditoria Lighthouse.
- Excluído: alterações de backend, pricing, campanhas de marketing, app móvel nativo, SEO técnico fora do necessário para CWV.

### 4.2 Contexto do estudo (tipo de organização, projeto, experiência)

Estudo acadêmico (PUC), projeto de baixa criticidade, conduzido por um pesquisador, com tráfego de teste/produção controlada. Participantes indiretos via tráfego real; experiência prévia em Front-End e métricas web.

### 4.3 Premissas

- GA4 e/ou CrUX configurados e acessíveis; permissão de coleta (consent) adequada.
- Ambiente estável o suficiente para medições comparáveis no período selecionado.
- Volume mínimo de sessões para análises segmentadas simples.

### 4.4 Restrições

- Tempo limitado e orçamento nulo/baixo; dependência de ferramentas gratuitas.
- Acesso controlado a ambientes e dados; políticas de privacidade e compliance.
- Amostragem e limites de coleta do GA4/CrUX.

### 4.5 Limitações previstas

- Validez externa limitada: contexto específico e amostra possivelmente pequena.
- Confundidores: sazonalidade, origem de tráfego, mudanças paralelas no produto.
- Dificuldade de isolar causalidade sem A/B amplo.

## 5. Stakeholders e impacto esperado

### 5.1 Stakeholders principais

- Desenvolvimento Front-End, QA, Produto, Gestão/Coordenação acadêmica, Usuários/participantes.

### 5.2 Interesses e expectativas dos stakeholders

- Dev Front-End: evidências acionáveis de gargalos e priorização de melhorias.
- QA: critérios objetivos de aceitação relacionados a CWV.
- Produto: impacto esperado em conversão e engajamento; priorização de roadmap.
- Gestão: viabilidade, custo/benefício e riscos.

### 5.3 Impactos potenciais no processo / produto

- Pequena sobrecarga de instrumentação; possíveis ajustes de prioridades e prazos.
- Mudanças de performance podem afetar experiência durante testes; comunicação necessária.

## 6. Riscos de alto nível, premissas e critérios de sucesso

### 6.1 Riscos de alto nível (negócio, técnicos, etc.)

- Baixo volume de dados; indisponibilidade de acessos; instabilidade de ambiente.
- Instrumentação incorreta; sampling/sessões insuficientes no GA4; viés de medição.
- Mudanças paralelas no produto mascarando efeitos.

### 6.2 Critérios de sucesso globais (go / no-go)

- Coleta válida por período mínimo (ex.: ≥ 2 semanas) com amostra suficiente.
- Estimativa do efeito de CWV em rejeição/conversão com significância prática/estatística.
- Lista priorizada de ações de otimização alinhada a impacto e esforço.

### 6.3 Critérios de parada antecipada (pré-execução)

- Falta de acesso a dados/ambiente; reprovação de privacidade/ética.
- Instabilidade severa do sistema; volume de tráfego insuficiente.
- Mudança de escopo que inviabilize comparabilidade das medições.

## 7. Modelo conceitual e hipóteses

### 7.1 Modelo conceitual do experimento

Qualidade de desempenho medida por Core Web Vitals (LCP, INP, CLS) influencia diretamente a experiência do usuário (fluidez, estabilidade e responsividade). Melhorias aplicadas em otimização (ex.: pré-carregamento de recursos críticos, lazy loading de imagens/componentes, redução de JS bloqueante, compressão e cache) tendem a melhorar os CWV, o que reduz atrito em páginas de entrada e fluxos críticos (cadastro/checkout), diminuindo a taxa de rejeição e aumentando a taxa de conversão.

### 7.2 Hipóteses formais (H0, H1)

- H0_Q2-LCP: A taxa de rejeição não difere entre buckets de LCP (bom/NI/ruim).
- H1_Q2-LCP: Buckets com LCP pior apresentam maior taxa de rejeição.
- H0_Q2-INP: A taxa de conversão não difere entre buckets de INP.
- H1_Q2-INP: Buckets com INP pior apresentam menor taxa de conversão.
- H0_Q2-CLS: A taxa de conversão é independente do nível de CLS.
- H1_Q2-CLS: Maior CLS está associado a menor taxa de conversão em páginas de checkout.
- H0_Q3-Efeito: Melhorias em LCP/INP/CLS não alteram rejeição/conversão.
- H1_Q3-Efeito: Melhorias em LCP/INP/CLS reduzem rejeição e aumentam conversão.

### 7.3 Nível de significância e considerações de poder

Nível de significância α = 0,05. Espera-se poder estatístico moderado a alto com janela de observação de 2–4 semanas, dependendo do volume de sessões por segmento (página/dispositivo/rede/origem). Para efeitos práticos (ex.: redução absoluta de 2–5 p.p. em rejeição ou aumento de 1–3 p.p. em conversão), serão priorizadas análises com estratificação e modelos que incorporem covariáveis, mitigando perda de poder por heterogeneidade.

## 8. Variáveis, fatores, tratamentos e objetos de estudo

### 8.1 Objetos de estudo

Páginas landing, listagem, detalhe e fluxo de conversão (cadastro/checkout); componentes críticos (hero, formulário, carrinho); recursos estáticos (imagens, CSS, JS) e sua configuração (hints, cache, compressão).

### 8.2 Sujeitos / participantes (visão geral)

Usuários reais (tráfego de produção controlada/teste), agregados por sessão; quando aplicável, estudantes/testadores para validações pontuais de laboratório.

### 8.3 Variáveis independentes (fatores) e seus níveis

- Bucket de LCP: bom / precisa melhorar / ruim.
- Bucket de INP: bom / precisa melhorar / ruim.
- Bucket de CLS: bom / precisa melhorar / ruim.
- Tipo de otimização aplicada: nenhuma (controle) / preload/preconnect / lazy loading / otimização de JS (code split, defer) / compressão/cache de ativos.

### 8.4 Tratamentos (condições experimentais)

- Controle: estado atual sem intervenções de performance relevantes.
- Tratamento 1: preload/preconnect de recursos críticos (ex.: fonte, CSS crítico).
- Tratamento 2: lazy loading de imagens/componentes não críticos.
- Tratamento 3: otimização de JS (divisão de código, defer/async), compressão e cache.
  Condições distinguem-se pela combinação de técnicas e pela página/fluxo alvo.

### 8.5 Variáveis dependentes (respostas)

Taxa de rejeição (%), Taxa de conversão (%), Engajamento (tempo médio na página, páginas por sessão), taxa de erro de interação (quando disponível).

### 8.6 Variáveis de controle / bloqueio

Tipo de dispositivo (mobile/desktop), classe de rede (3G/4G/Wi-Fi), tipo de página, origem de tráfego, horário/dia, presença de cache, versão de conteúdo.

### 8.7 Possíveis variáveis de confusão conhecidas

Sazonalidade, campanhas de marketing, mudanças paralelas de UI/funcionalidades, mix de usuários, consentimento/privacidade, uso de ad-blockers.

## 9. Desenho experimental

### 9.1 Tipo de desenho (completamente randomizado, blocos, fatorial, etc.)

Desenho observacional correlacional com blocos por página/dispositivo/rede e, quando viável, desenho quasi-experimental A/B. Para múltiplas técnicas aplicadas em conjunto, considera-se abordagem fatorial limitada em páginas-alvo.

### 9.2 Randomização e alocação

Em A/B, alocação aleatória por sessão (ex.: 50/50) usando mecanismo de experimento do cliente/analytics; preservação de coortes durante a janela de medição. Em observacional, não há randomização, apenas estratificação e ajuste por covariáveis.

### 9.3 Balanceamento e contrabalanço

Garantia de comparabilidade por segmento (página/dispositivo/rede/origem) via quotas ou ponderação; monitoramento de tamanhos de amostra e taxas. Em fluxos com etapas sequenciais, contrabalanço por ordem quando aplicável em testes de laboratório.

### 9.4 Número de grupos e sessões

Dois grupos principais (controle e tratamento) e até três braços de tratamento conforme 8.4. Janela de coleta de 2–4 semanas por grupo, buscando amostra suficiente para estimar efeitos com α = 0,05.

## 10. População, sujeitos e amostragem

### 10.1 População-alvo

Usuários de aplicações web Front-End (desktop e mobile) acessando páginas de landing, listagem, detalhe e conversão em ambiente acadêmico (PUC), além de estudantes/testadores envolvidos em validações de laboratório.

### 10.2 Critérios de inclusão de sujeitos

- Sessões com consentimento válido para coleta.
- Navegadores suportados (Chrome/Edge/Firefox recentes) com execução de `web-vitals` e GA4.
- Dispositivos mobile e desktop com rede estável suficiente para interação.

### 10.3 Critérios de exclusão de sujeitos

- Bots/crawlers, tráfego administrativo/interno e sessões sem consentimento.
- Navegadores ou configurações que bloqueiam scripts essenciais (ad-blockers agressivos, no-script), quando inviabilizam medição.
- Conexões extremamente instáveis ou erros que impedem carregar/instrumentar a página.

### 10.4 Tamanho da amostra planejado (por grupo)

Planejado: ≥ 300 sessões por grupo (controle/tratamento) no período de 2–4 semanas, com meta de ≥ 100 sessões por segmento principal (página/dispositivo). Ajustes conforme tráfego real e poder necessário para detectar efeitos práticos.

### 10.5 Método de seleção / recrutamento

Tráfego natural (amostra de conveniência) com alocação aleatória por sessão em A/B quando aplicável. Para laboratório, convite aberto à turma/disciplina com slots definidos.

### 10.6 Treinamento e preparação dos sujeitos

Materiais curtos com objetivos do estudo, consentimento, política de privacidade, instruções de uso das páginas de teste e nota sobre comportamento esperado; em laboratório, roteiro de tarefas e guia rápido.

## 11. Instrumentação e protocolo operacional

### 11.1 Instrumentos de coleta (questionários, logs, planilhas, etc.)

- `web-vitals`: coleta de LCP/INP/CLS em campo (RUM).
- GA4: rejeição, conversão, eventos de interação e segmentos.
- CrUX: distribuição populacional externa de CWV.
- Lighthouse/PageSpeed: auditorias e diagnósticos (TTFB, peso, bloqueios, imagens).
- Planilhas/BigQuery: agregação, limpeza e análise.
- Scripts ETL: export/import e transformação de dados para tabelas de análise.

### 11.2 Materiais de suporte (instruções, guias)

Guia de operação, checklist de instrumentação, instruções de consentimento, roteiro de tarefas (lab), templates de coleta e planilhas com dicionário de métricas.

### 11.3 Procedimento experimental (protocolo – visão passo a passo)

1. Preparar páginas-alvo e instrumentação (`web-vitals`, GA4).
2. Validar coleta em ambiente de teste; publicar em produção controlada.
3. Definir janelas e segmentos (página/dispositivo/rede/origem).
4. Executar coleta contínua por 2–4 semanas; monitorar integridade.
5. Rodar auditorias Lighthouse; registrar diagnósticos.
6. Exportar dados para planilhas/BigQuery; aplicar ETL padronizado.
7. Analisar conforme GQM (Q1–Q4); gerar visualizações e tabelas.
8. Consolidar resultados e recomendações; revisar com stakeholders.
9. Encerrar coleta; arquivar dados e documentação.

### 11.4 Plano de piloto (se haverá piloto, escopo e critérios de ajuste)

Piloto de 3–5 dias em 1–2 páginas (landing e checkout) com amostra reduzida. Critérios: integridade da coleta, estabilidade de métricas, ausência de regressões visíveis. Ajustes: correção de instrumentação, segmentação, thresholds e protocolo.

### 11.5 Fluxograma operacional (passo a passo)

```
INÍCIO
  |
  v
Planejamento e desenho (GQM, escopo, stakeholders)
  - Stakeholders: Produto, Dev Front-End, QA, Gestão
  - Variáveis: independentes (buckets LCP/INP/CLS), controle (dispositivo, rede, página, origem, horário)
  - Métricas: LCP, INP, CLS, FCP, TBT, TTFB, JS bytes, CSS bytes, nº requisições, rejeição, conversão
  |
  v
Instrumentação e configuração
  - Instrumentos: web-vitals (RUM), GA4 (eventos, rejeição, conversão)
  - Suporte: CrUX (distribuições), Lighthouse/PageSpeed (auditorias)
  |
  v
Piloto (3–5 dias)
  - Validação: integridade de coleta, estabilidade de métricas
  - Ajustes: segmentação, thresholds, correção de instrumentação
  |
  v
Coleta contínua (2–4 semanas)
  - Dados: sessões por página/dispositivo/rede/origem
  - Monitoramento: qualidade dos dados, erros de coleta
  |
  v
Auditorias de performance
  - Lighthouse/PageSpeed: TTFB, peso de JS/CSS, bloqueios, imagens
  - Saídas: oportunidades e diagnósticos
  |
  v
ETL e preparação de dados
  - Ferramentas: Planilhas/BigQuery, scripts ETL
  - Passos: limpeza, agregação, criação de tabelas por segmentos
  |
  v
Análise GQM
  - Q1: Distribuições de LCP/INP/CLS por segmentos
  - Q2: Rejeição/Conversão por buckets de CWV
  - Q3: Modelagem de efeito (regressão; A/B quando aplicável)
  - Q4: Diagnóstico e ranking de ações (correlações + auditorias)
  |
  v
Recomendações de otimização
  - Ações: preload/preconnect, lazy loading, code split/defer, compressão/cache
  - Priorização: impacto vs. esforço
  |
  v
Revisão com stakeholders
  - Produto/Dev/QA/Gestão: decisão de go/no-go
  - Critérios: coleta válida, efeito estimado, lista priorizada
  |
  v
Implementação (se aprovado) e monitoramento
  - Execução de melhorias + coleta pós-ação
  - Verificação de impacto em CWV e negócio
  |
  v
Encerramento
  - Arquivamento: dados, relatórios, documentação do experimento
  - Lições aprendidas e próximos passos
```

## 12. Plano de análise de dados (pré-execução)

### 12.1 Estratégia geral de análise (como responderá às questões)

Aplicar o mapeamento GQM: Q1 (distribuições por segmento); Q2 (comparações de rejeição/conversão por buckets de CWV); Q3 (modelagem de efeito de melhorias em CWV sobre rejeição/conversão); Q4 (diagnóstico de causas e ranking de ações via auditorias e correlações).

### 12.2 Métodos estatísticos planejados

- Comparações entre grupos/buckets: ANOVA/Kruskal-Wallis para métricas contínuas; testes de proporção/qui-quadrado para rejeição/conversão.
- Modelagem: regressão logística (conversão), regressão linear/quantílica (LCP/INP/CLS), modelos com covariáveis (página, dispositivo, rede, origem).
- A/B: teste de diferença de proporções e intervalos de confiança; quando suposições não atendidas, testes não paramétricos e bootstrap.

### 12.3 Tratamento de dados faltantes e outliers

- Dados faltantes: exclusão listwise de sessões sem métricas críticas (LCP/INP/CLS) ou sem eventos necessários (conversão), com relatório de taxas de falta.
- Outliers: regras pré-definidas (winsorização em P99, IQR×3 ou limites técnicos plausíveis) e análise de sensibilidade com e sem outliers.
- Logs de decisões: registro das transformações para reprodutibilidade.

### 12.4 Plano de análise para dados qualitativos (se houver)

Coleta opcional de comentários/observações em laboratório; análise por codificação temática simples (usabilidade, performance percebida, frustração), categorização e contagem, triangulando com métricas quantitativas.

## 13. Avaliação de validade (ameaças e mitigação)

### 13.1 Validade de conclusão

**Ameaças identificadas:**

- **Baixo poder estatístico**: Amostra insuficiente para detectar efeitos práticos, especialmente em segmentos menores (página/dispositivo/rede). Mitigação: cálculo prévio de poder com base em estimativas conservadoras; extensão da janela de coleta se necessário; agregação de segmentos similares quando estatisticamente justificável; uso de testes não paramétricos quando apropriado.

- **Violação de suposições estatísticas**: Normalidade, homocedasticidade e independência das observações podem não ser atendidas. Mitigação: verificação de suposições (testes de normalidade, gráficos de resíduos); uso de testes robustos (Kruskal-Wallis, bootstrap); transformações quando aplicável (log, raiz quadrada); modelos que relaxam suposições (regressão quantílica).

- **Erros de medida**: Instrumentação incorreta, valores faltantes sistemáticos, viés de coleta (ad-blockers, navegadores não suportados). Mitigação: validação da instrumentação em piloto; comparação cruzada com CrUX quando disponível; auditorias Lighthouse periódicas; relatório de taxas de dados faltantes e análise de sensibilidade; filtros para excluir medições inválidas (valores negativos, extremos tecnicamente impossíveis).

- **Viés de seleção na amostra**: Tráfego não representativo, exclusão sistemática de segmentos. Mitigação: documentação clara de critérios de inclusão/exclusão; análise de representatividade comparando distribuições com CrUX; estratificação por variáveis de controle; ponderação quando necessário.

### 13.2 Validade interna

**Ameaças identificadas:**

- **History (história)**: Mudanças paralelas no produto, campanhas de marketing, sazonalidade durante o período de coleta. Mitigação: registro de mudanças de produto/marketing no período; análise de tendências temporais; comparação com períodos anteriores quando disponível; controle por covariáveis de tempo (dia da semana, horário).

- **Maturation (maturação)**: Mudanças naturais no comportamento do usuário ao longo do tempo, aprendizado ou fadiga. Mitigação: janela de coleta limitada (2–4 semanas) para reduzir efeitos de longo prazo; análise de coortes por data de primeira visita; estratificação temporal.

- **Selection (seleção)**: Diferenças sistemáticas entre grupos de controle e tratamento não atribuíveis ao tratamento. Mitigação: randomização em A/B quando viável; estratificação por variáveis de controle (dispositivo, rede, página, origem); modelos com covariáveis; análise de balanceamento pré-tratamento.

- **Mortality (mortalidade)**: Perda diferencial de participantes entre grupos. Mitigação: monitoramento de taxas de abandono por grupo; análise de características dos que permanecem vs. abandonam; testes de sensibilidade assumindo diferentes cenários de perda.

- **Instrumentation (instrumentação)**: Mudanças nos instrumentos de medida durante o experimento. Mitigação: padronização de versões de ferramentas (web-vitals, GA4); validação periódica da coleta; documentação de mudanças e análise de impacto.

- **Testing (teste)**: Efeitos de pré-teste ou pós-teste. Mitigação: uso de grupos de controle; análise de primeiras vs. subsequentes interações quando relevante.

### 13.3 Validade de constructo

**Ameaças identificadas:**

- **Ambiguidade de constructo**: LCP, INP e CLS podem não capturar completamente a experiência de performance percebida pelo usuário. Mitigação: uso de métricas complementares (FCP, TBT, Speed Index) para triangulação; validação com literatura estabelecida (definições oficiais do Chrome/Web.dev); comparação com métricas de negócio (rejeição, conversão) para validade preditiva.

- **Operacionalização inadequada**: Buckets de CWV (Good/NI/Poor) podem não refletir diferenças práticas significativas. Mitigação: uso de limiares oficiais recomendados; análise de sensibilidade com diferentes thresholds; análise contínua além de categórica quando apropriado.

- **Viés de medida**: Métricas de rejeição e conversão podem ser afetadas por fatores não relacionados a performance. Mitigação: definição clara e operacional de rejeição/conversão; controle por variáveis de confusão (origem de tráfego, tipo de página); análise de correlações parciais.

- **Efeito de expectativa**: Conhecimento prévio sobre CWV pode influenciar interpretação. Mitigação: análise cega quando possível; uso de critérios objetivos pré-definidos; revisão por pares.

### 13.4 Validade externa

**Ameaças identificadas:**

- **População limitada**: Amostra de contexto acadêmico (PUC) pode não representar usuários de produção comercial. Mitigação: documentação clara do contexto e limitações; comparação com dados públicos (CrUX) quando possível; replicação em outros contextos se viável.

- **Contexto específico**: Páginas, dispositivos e redes testadas podem não representar a diversidade real. Mitigação: estratificação por múltiplos segmentos (página, dispositivo, rede); análise de heterogeneidade de efeitos; documentação de características do contexto.

- **Temporalidade**: Resultados podem ser específicos ao período de coleta. Mitigação: documentação de condições temporais; análise de estabilidade temporal; replicação em diferentes períodos se possível.

- **Interação de seleção e tratamento**: Efeitos podem variar por características dos participantes. Mitigação: análise de subgrupos; modelos de interação; relatório de heterogeneidade.

### 13.5 Resumo das principais ameaças e estratégias de mitigação

| Ameaça                       | Tipo de Validade | Severidade | Estratégia de Mitigação Principal                                   |
| ---------------------------- | ---------------- | ---------- | ------------------------------------------------------------------- |
| Baixo poder estatístico      | Conclusão        | Alta       | Cálculo prévio de poder, extensão de janela, agregação de segmentos |
| Violação de suposições       | Conclusão        | Média      | Verificação de suposições, testes robustos, transformações          |
| Erros de medida              | Conclusão        | Alta       | Validação em piloto, comparação com CrUX, filtros de qualidade      |
| History (mudanças paralelas) | Interna          | Alta       | Registro de mudanças, análise temporal, controle por covariáveis    |
| Selection (seleção)          | Interna          | Média      | Randomização, estratificação, modelos com covariáveis               |
| Ambiguidade de constructo    | Constructo       | Média      | Métricas complementares, validação com literatura, triangulação     |
| População limitada           | Externa          | Alta       | Documentação de contexto, comparação com CrUX, replicação           |
| Contexto específico          | Externa          | Média      | Estratificação múltipla, análise de heterogeneidade                 |

## 14. Ética, privacidade e conformidade

### 14.1 Questões éticas (uso de sujeitos, incentivos, etc.)

**Questões identificadas:**

- **Participação não voluntária**: Usuários de tráfego natural não são explicitamente recrutados, mas seus dados são coletados. Mitigação: implementação de consentimento informado via banner/cookie consent conforme LGPD; opção de opt-out; transparência sobre coleta e uso de dados.

- **Uso de estudantes em laboratório**: Participantes podem sentir pressão para participar em contexto acadêmico. Mitigação: participação voluntária e anônima; esclarecimento de que não há impacto acadêmico negativo por não participar; ausência de incentivos coercitivos.

- **Riscos de exposição**: Dados de performance podem revelar padrões de uso ou comportamento. Mitigação: agregação de dados (sem identificação individual); anonimização/pseudoanonimização; acesso restrito a dados brutos.

- **Impacto na experiência do usuário**: Instrumentação ou testes podem afetar performance ou funcionalidade. Mitigação: instrumentação leve e não intrusiva; testes em ambiente controlado quando possível; monitoramento de regressões.

### 14.2 Consentimento informado

**Processo de consentimento:**

- **Para tráfego natural**: Banner/cookie consent informando sobre coleta de métricas de performance (CWV) e dados analíticos (GA4) para fins de pesquisa acadêmica; link para política de privacidade detalhada; opção de recusar cookies não essenciais (respeitando que alguns dados podem não ser coletados).

- **Para participantes de laboratório**: Formulário de consentimento informado explicando objetivos do estudo, procedimentos, riscos mínimos, benefícios (contribuição para pesquisa), direito de retirada, confidencialidade e contato do pesquisador; assinatura ou aceite digital antes da participação.

- **Conteúdo do consentimento**: Objetivos do experimento, tipos de dados coletados (métricas de performance, eventos de navegação), duração da coleta, uso dos dados (análise acadêmica, publicação), medidas de proteção, direitos dos participantes (acesso, retificação, exclusão conforme LGPD).

### 14.3 Privacidade e proteção de dados

**Dados coletados:**

- **Dados de performance**: LCP, INP, CLS, FCP, TBT, TTFB (valores numéricos agregados por sessão).
- **Dados analíticos**: Eventos de navegação, páginas visitadas, origem de tráfego, tipo de dispositivo/rede (agregados).
- **Dados não coletados**: Informações pessoais identificáveis (nome, e-mail, CPF), conteúdo de formulários, dados de pagamento.

**Medidas de proteção:**

- **Anonimização**: Remoção de identificadores diretos; agregação por sessão anônima; uso de IDs de sessão não vinculáveis a usuários.
- **Pseudoanonimização**: IDs de sessão gerados aleatoriamente; sem vinculação a contas ou perfis.
- **Controle de acesso**: Acesso restrito a dados brutos apenas ao pesquisador responsável; dados agregados para análise; armazenamento em ambiente seguro (Google Cloud com controles de acesso).
- **Retenção**: Dados mantidos pelo período necessário para análise e publicação (máximo 2 anos); exclusão após conclusão do trabalho; arquivamento de dados agregados anonimizados para replicação se necessário.

**Conformidade:**

- **LGPD**: Conformidade com Lei Geral de Proteção de Dados (consentimento, finalidade, minimização, segurança, transparência).
- **Política de privacidade**: Documento público descrevendo práticas de coleta, uso e proteção de dados.

### 14.4 Aprovações necessárias (comitê de ética, jurídico, DPO, etc.)

**Aprovações requeridas:**

- **Comitê de Ética em Pesquisa (CEP) da PUC**: Submissão do protocolo de pesquisa com foco em aspectos éticos e de privacidade; status: pendente (a ser submetido antes do início da coleta).

- **Coordenação do Curso/Disciplina**: Aprovação do trabalho final como projeto de pesquisa; status: em andamento.

- **Data Protection Officer (DPO) / Área Jurídica (se aplicável)**: Revisão de conformidade com LGPD e políticas institucionais; status: pendente.

- **Gestão de TI/Infraestrutura**: Aprovação para uso de ferramentas (GA4, BigQuery) e acesso a ambientes; status: pendente.

**Plano de submissão:**

1. Preparar protocolo completo com seções de ética e privacidade.
2. Submeter ao CEP da PUC com documentação necessária (termo de consentimento, política de privacidade).
3. Aguardar aprovação antes de iniciar coleta de dados.
4. Obter aprovações complementares (jurídico, TI) conforme necessário.

## 15. Recursos, infraestrutura e orçamento

### 15.1 Recursos humanos e papéis

| Papel                             | Responsável                          | Responsabilidades Principais                                     |
| --------------------------------- | ------------------------------------ | ---------------------------------------------------------------- |
| Pesquisador Principal (PI)        | Marcus Vinícius Carvalho de Oliveira | Desenho do experimento, instrumentação, coleta, análise, redação |
| Orientador/Professor              | A definir                            | Revisão do plano, orientação metodológica, aprovação acadêmica   |
| Desenvolvedor Front-End (suporte) | A definir (se disponível)            | Implementação de instrumentação, ajustes técnicos                |
| Stakeholders (consultivos)        | Produto, QA, Gestão                  | Revisão de objetivos, validação de resultados, priorização       |

**Observação**: Projeto individual acadêmico; suporte de stakeholders é consultivo e não dedicado.

### 15.2 Infraestrutura técnica necessária

**Ambientes:**

- Ambiente de desenvolvimento/teste: para validação de instrumentação e piloto.
- Ambiente de produção controlada: para coleta de dados reais (se disponível).

**Ferramentas e serviços:**

- **Biblioteca `web-vitals`**: Open source, gratuita (npm).
- **Google Analytics 4 (GA4)**: Conta gratuita com limites de eventos (até 10 milhões de eventos/mês).
- **Chrome UX Report (CrUX)**: API pública gratuita (com limites de rate).
- **Lighthouse/PageSpeed Insights**: Ferramentas gratuitas (CLI e web).
- **BigQuery**: Conta gratuita com 10 GB de armazenamento e 1 TB de processamento/mês (suficiente para análise).
- **Planilhas Google Sheets**: Gratuito, para análises intermediárias.

**Repositórios:**

- Repositório Git (GitHub/GitLab): para versionamento de scripts, instrumentação e documentação.

**Integrações:**

- Integração GA4 → BigQuery (export automático, se configurado).
- Scripts ETL (Python/JavaScript) para transformação de dados.

### 15.3 Materiais e insumos

**Materiais digitais:**

- Licenças: nenhuma requerida (uso de ferramentas gratuitas).
- Templates e formulários: consentimento informado, política de privacidade, checklist de instrumentação, planilhas de análise.
- Documentação: guias de operação, dicionário de métricas, protocolo de análise.

**Dispositivos (para testes de laboratório, se aplicável):**

- Dispositivos móveis e desktop para validação (próprios do pesquisador ou emprestados).
- Conexões de rede variadas (Wi-Fi, 4G) para testes de segmentação.

**Observação**: Projeto de baixo custo, utilizando principalmente ferramentas gratuitas e recursos próprios.

### 15.4 Orçamento e custos estimados

| Item                              | Custo Estimado                               | Fonte de Financiamento                   |
| --------------------------------- | -------------------------------------------- | ---------------------------------------- |
| Horas do pesquisador              | 80–120 horas (trabalho acadêmico)            | Sem custo (trabalho final)               |
| Ferramentas (GA4, BigQuery, etc.) | R$ 0 (uso gratuito dentro dos limites)       | N/A                                      |
| Infraestrutura de hospedagem      | R$ 0 (uso de ambiente existente ou gratuito) | N/A                                      |
| Licenças de software              | R$ 0 (open source/gratuito)                  | N/A                                      |
| Materiais e insumos               | R$ 0 (digitais, sem custo)                   | N/A                                      |
| **Total estimado**                | **R$ 0**                                     | **Trabalho acadêmico sem financiamento** |

**Observações:**

- Projeto sem orçamento alocado; dependência de ferramentas gratuitas e trabalho do pesquisador.
- Se limites de ferramentas gratuitas forem excedidos, pode ser necessário ajustar escopo ou buscar alternativas.
- Custos potenciais não previstos: hospedagem adicional se ambiente próprio não estiver disponível (estimativa: R$ 20–50/mês para serviço básico, se necessário).

## 16. Cronograma, marcos e riscos operacionais

### 16.1 Macrocronograma (até o início da execução)

| Marco                           | Data Planejada          | Descrição                                                        |
| ------------------------------- | ----------------------- | ---------------------------------------------------------------- |
| Conclusão do plano experimental | 21/11/2025              | Finalização do documento de plano (versão v1.0)                  |
| Submissão ao CEP                | 28/11/2025              | Envio do protocolo para Comitê de Ética                          |
| Aprovação ética                 | 15/12/2025 (estimativa) | Aprovação do CEP (assumindo 2–3 semanas)                         |
| Preparação de instrumentação    | 16/12/2025 – 05/01/2026 | Implementação de web-vitals, configuração GA4, validação técnica |
| Piloto                          | 06/01/2026 – 10/01/2026 | Execução do piloto (3–5 dias)                                    |
| Revisão pós-piloto              | 11/01/2026 – 15/01/2026 | Ajustes baseados no piloto                                       |
| Aprovação final para execução   | 16/01/2026              | Go/no-go com stakeholders                                        |
| **Início da coleta contínua**   | **17/01/2026**          | **Início da operação principal (2–4 semanas)**                   |

**Observação**: Datas são estimativas e podem ser ajustadas conforme aprovações e disponibilidade.

### 16.2 Dependências entre atividades

**Dependências críticas:**

- **Instrumentação → Piloto**: Preparação técnica deve estar completa antes do piloto.
- **Aprovação ética → Coleta**: Nenhuma coleta de dados pode iniciar sem aprovação do CEP.
- **Piloto → Coleta contínua**: Ajustes do piloto devem ser implementados antes da coleta principal.
- **Aprovação de stakeholders → Coleta contínua**: Go/no-go necessário antes da operação.
- **Configuração GA4 → Coleta**: GA4 deve estar configurado e validado antes da coleta.

**Dependências de suporte:**

- **Orientação → Plano**: Revisão do orientador antes da submissão ao CEP.
- **Acesso a ambiente → Instrumentação**: Acesso a ambiente de teste/produção necessário para instrumentação.

### 16.3 Riscos operacionais e plano de contingência

| Risco                                           | Probabilidade | Impacto | Plano de Contingência                                                                                                     |
| ----------------------------------------------- | ------------- | ------- | ------------------------------------------------------------------------------------------------------------------------- |
| Atraso na aprovação do CEP                      | Média         | Alto    | Iniciar preparação técnica em paralelo; ajustar cronograma; considerar simplificação do protocolo se necessário           |
| Indisponibilidade de ambiente                   | Baixa         | Alto    | Usar ambiente de teste próprio; considerar ferramentas de staging; ajustar escopo se necessário                           |
| Volume de tráfego insuficiente                  | Média         | Médio   | Estender janela de coleta; reduzir segmentação; usar dados sintéticos para validação metodológica (com limitações claras) |
| Problemas técnicos na instrumentação            | Média         | Médio   | Validação extensiva em piloto; ter scripts de fallback; usar múltiplas fontes de dados (GA4 + CrUX)                       |
| Indisponibilidade de ferramentas (GA4/BigQuery) | Baixa         | Alto    | Ter alternativas (CrUX, planilhas); considerar ferramentas open source (Plausible, Matomo) se viável                      |
| Mudanças de escopo durante execução             | Baixa         | Médio   | Processo de controle de mudanças (seção 17.3); avaliação de impacto antes de aprovar mudanças                             |
| Conflitos de agenda do pesquisador              | Média         | Baixo   | Planejamento flexível; priorização de atividades críticas; extensão de prazo se necessário                                |

**Ações preventivas:**

- Iniciar submissão ao CEP o mais cedo possível.
- Validar acesso a ferramentas e ambientes antes do início.
- Manter comunicação próxima com stakeholders para antecipar problemas.
- Ter plano B para cada componente crítico.

## 17. Governança do experimento

### 17.1 Papéis e responsabilidades formais

| Papel                                    | Responsabilidade                                       | Autoridade                                                 |
| ---------------------------------------- | ------------------------------------------------------ | ---------------------------------------------------------- |
| **Pesquisador Principal (PI)**           | Execução do experimento, coleta, análise, documentação | Decisões operacionais diárias, ajustes técnicos            |
| **Orientador**                           | Revisão metodológica, orientação acadêmica             | Aprovação de mudanças metodológicas significativas         |
| **Comitê de Ética (CEP)**                | Avaliação ética e de privacidade                       | Aprovação/reprovação do protocolo, autorização para coleta |
| **Stakeholders (Produto/Dev/QA/Gestão)** | Revisão de objetivos e resultados                      | Go/no-go para execução, priorização de recomendações       |
| **Coordenação Acadêmica**                | Aprovação do trabalho final                            | Validação acadêmica do projeto                             |

**Fluxo de responsabilidade:**

- **Decisões operacionais**: PI (com consulta ao orientador quando necessário).
- **Mudanças de escopo/metodologia**: PI propõe → Orientador revisa → Stakeholders aprovam (se impacto significativo).
- **Aprovação ética**: CEP (obrigatório antes da coleta).
- **Go/no-go para execução**: Stakeholders + Orientador (após piloto e revisão).

### 17.2 Ritos de acompanhamento pré-execução

| Rito                            | Frequência                   | Participantes                           | Objetivo                                           |
| ------------------------------- | ---------------------------- | --------------------------------------- | -------------------------------------------------- |
| Revisão do plano com orientador | Uma vez (antes da submissão) | PI, Orientador                          | Validação metodológica e acadêmica                 |
| Submissão e acompanhamento CEP  | Conforme necessário          | PI, CEP                                 | Aprovação ética                                    |
| Checkpoint pós-piloto           | Uma vez (após piloto)        | PI, Orientador, Stakeholders (opcional) | Revisão de resultados do piloto, ajustes, go/no-go |
| Revisão final pré-execução      | Uma vez (antes da coleta)    | PI, Orientador, Stakeholders principais | Aprovação final para início da operação            |

**Comunicação contínua:**

- Atualizações semanais ao orientador durante preparação (se solicitado).
- Comunicação ad-hoc com stakeholders em caso de bloqueios ou mudanças significativas.

### 17.3 Processo de controle de mudanças no plano

**Tipos de mudanças:**

- **Mudanças menores** (ajustes técnicos, correções, melhorias de clareza): Aprovação do PI; documentação no histórico de versão do documento.
- **Mudanças moderadas** (ajustes de escopo funcional, métricas adicionais, extensão de prazo): Proposta do PI → Revisão do orientador → Aprovação se alinhado com objetivos.
- **Mudanças maiores** (mudança de objetivos, metodologia, escopo significativo): Proposta do PI → Revisão do orientador → Consulta a stakeholders → Aprovação formal; atualização de versão do documento (v1.1, v1.2, etc.).

**Processo formal:**

1. **Proposta**: PI documenta a mudança proposta (razão, impacto, alternativas).
2. **Análise**: Orientador e stakeholders relevantes avaliam impacto metodológico, ético e operacional.
3. **Decisão**: Aprovação ou rejeição com justificativa.
4. **Registro**: Mudança documentada no histórico de versão do plano; atualização do documento.

**Registro de mudanças:**

- Histórico de versão na seção 1.3 do documento.
- Log de decisões em repositório Git (commits com mensagens descritivas).

## 18. Plano de documentação e reprodutibilidade

### 18.1 Repositórios e convenções de nomeação

**Repositório principal:**

- **Localização**: GitHub/GitLab (repositório privado ou público conforme política institucional).
- **Estrutura proposta**:
  ```
  /docs
    - README.md (este documento)
    - protocolo-etica.md
    - politica-privacidade.md
    - guia-operacao.md
  /instrumentation
    - web-vitals-setup.js
    - ga4-config.json
  /scripts
    - etl/
      - extract-ga4.py
      - transform-cwv.py
      - load-bigquery.py
    - analysis/
      - q1-distributions.R (ou .py)
      - q2-correlation.R
      - q3-modeling.R
      - q4-diagnostics.R
  /data
    - raw/ (dados brutos, não versionados, acesso restrito)
    - processed/ (dados agregados anonimizados)
    - results/ (tabelas e visualizações finais)
  /templates
    - consentimento-informado.md
    - checklist-instrumentacao.md
  ```

**Convenções de nomeação:**

- **Arquivos de código**: `kebab-case` (ex: `extract-ga4-data.py`).
- **Arquivos de dados**: `YYYY-MM-DD-description.csv` (ex: `2026-01-17-cwv-sessions.csv`).
- **Versões de documentos**: `v1.0`, `v1.1`, etc. no nome do arquivo e no conteúdo.
- **Branches Git**: `feature/descricao`, `fix/descricao`, `docs/descricao`.

### 18.2 Templates e artefatos padrão

**Templates disponíveis:**

- **Termo de Consentimento Informado**: Template em Markdown com seções padrão (objetivos, procedimentos, riscos, direitos).
- **Política de Privacidade**: Template descrevendo coleta, uso, proteção e direitos conforme LGPD.
- **Checklist de Instrumentação**: Lista de verificação para validação técnica antes do piloto e coleta.
- **Planilha de Análise GQM**: Template com abas para cada questão (Q1–Q4) e métricas associadas.
- **Roteiro de Tarefas (Laboratório)**: Guia para participantes de testes de laboratório (se aplicável).
- **Dicionário de Métricas**: Documento de referência com definições, unidades, limiares e fontes de todas as métricas.

**Localização**: Pasta `/templates` no repositório.

### 18.3 Plano de empacotamento para replicação futura

**Componentes para replicação:**

- **Documentação completa**: Plano experimental (este documento), protocolo de ética aprovado, guia de operação, dicionário de métricas.
- **Código instrumentação**: Scripts de instrumentação (`web-vitals`, GA4) com comentários e README de instalação.
- **Scripts ETL e análise**: Código reprodutível (Python/R) com dependências documentadas (`requirements.txt`, `renv.lock`), exemplos de dados sintéticos para teste.
- **Dados de exemplo**: Dataset agregado anonimizado representativo (sem dados pessoais) para validação de scripts.
- **Instruções de replicação**: README específico (`REPLICATION.md`) com passo a passo: pré-requisitos, configuração, execução, interpretação de resultados.

**Formato de empacotamento:**

- Repositório Git com tags de versão (ex: `v1.0-final`).
- Arquivo `REPLICATION.md` na raiz com instruções completas.
- Dados de exemplo em formato aberto (CSV, JSON).
- Licença apropriada (ex: MIT para código, CC-BY para dados/documentação, se aplicável).

**Critérios de qualidade para replicação:**

- Código executável sem dependências não documentadas.
- Resultados reproduzíveis com dados de exemplo.
- Documentação clara de limitações e pré-requisitos.

## 19. Plano de comunicação

### 19.1 Públicos e mensagens-chave pré-execução

| Público                                  | Mensagens-Chave                                                         | Objetivo da Comunicação                          |
| ---------------------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------ |
| **Orientador**                           | Objetivos do experimento, metodologia, cronograma, status de aprovações | Alinhamento acadêmico, revisão metodológica      |
| **Stakeholders (Produto/Dev/QA/Gestão)** | Objetivos, escopo, impacto esperado, cronograma, necessidade de apoio   | Engajamento, validação de objetivos, go/no-go    |
| **Comitê de Ética (CEP)**                | Protocolo completo, aspectos éticos, privacidade, consentimento         | Aprovação ética obrigatória                      |
| **Coordenação Acadêmica**                | Projeto de trabalho final, objetivos, metodologia                       | Aprovação acadêmica do trabalho                  |
| **Participantes (se laboratório)**       | Objetivos, procedimentos, consentimento, privacidade                    | Consentimento informado, participação voluntária |

**Mensagens principais:**

- **Objetivo**: Analisar relação entre Core Web Vitals e métricas de negócio (rejeição, conversão).
- **Escopo**: Páginas Front-End (landing, listagem, detalhe, conversão); coleta de campo (RUM) e auditorias.
- **Impacto esperado**: Evidências para priorização de otimizações de performance.
- **Cronograma**: Coleta de 2–4 semanas após aprovações e piloto.
- **Privacidade**: Conformidade com LGPD, dados anonimizados, consentimento informado.

### 19.2 Canais e frequência de comunicação

| Canal                           | Público                                | Frequência                                          | Formato                                     |
| ------------------------------- | -------------------------------------- | --------------------------------------------------- | ------------------------------------------- |
| **E-mail**                      | Orientador, Stakeholders, CEP          | Conforme necessário (eventos, bloqueios)            | Formal, documentado                         |
| **Reuniões síncronas**          | Orientador, Stakeholders (checkpoints) | 2–3 vezes (revisão plano, pós-piloto, pré-execução) | Presencial ou online (gravadas se possível) |
| **Slack/Teams** (se disponível) | Equipe técnica (Dev Front-End)         | Ad-hoc (dúvidas técnicas)                           | Informal, rápido                            |
| **Documentação compartilhada**  | Todos (via repositório)                | Contínua (atualizações do plano)                    | Markdown, versionado                        |

**Preferências:**

- Comunicação formal (e-mail) para aprovações e decisões importantes.
- Documentação no repositório para transparência e histórico.
- Reuniões síncronas para discussões complexas e alinhamento.

### 19.3 Pontos de comunicação obrigatórios

| Evento                               | Público                                       | Prazo                            | Formato                                         |
| ------------------------------------ | --------------------------------------------- | -------------------------------- | ----------------------------------------------- |
| **Submissão do plano ao CEP**        | CEP                                           | Imediato após conclusão do plano | Formulário oficial + documentos anexos          |
| **Aprovação ética recebida**         | Orientador, Stakeholders                      | Imediato após recebimento        | E-mail com cópia da aprovação                   |
| **Conclusão do piloto**              | Orientador, Stakeholders                      | Imediato após piloto             | Relatório breve (resultados, ajustes, go/no-go) |
| **Decisão de go/no-go**              | Todos os stakeholders                         | Antes do início da coleta        | E-mail formal + registro no repositório         |
| **Mudanças significativas no plano** | Orientador, Stakeholders, CEP (se necessário) | Imediato após decisão            | E-mail + atualização do documento               |
| **Adiamento ou cancelamento**        | Todos os stakeholders                         | Imediato após decisão            | E-mail formal com justificativa                 |
| **Início da coleta**                 | Orientador, Stakeholders                      | No dia do início                 | Notificação breve (e-mail)                      |

**Registro de comunicações:**

- E-mails importantes arquivados no repositório (`/docs/comunicacoes/`).
- Decisões documentadas no histórico de versão do plano.

## 20. Critérios de prontidão para execução (Definition of Ready)

### 20.1 Checklist de prontidão (itens que devem estar completos)

**Aprovações e conformidade:**

- [ ] Aprovação do Comitê de Ética (CEP) recebida e documentada.
- [ ] Aprovação do orientador para início da execução.
- [ ] Go/no-go dos stakeholders principais (Produto/Dev/QA/Gestão) obtido.
- [ ] Conformidade com LGPD verificada (política de privacidade publicada, consentimento implementado).

**Preparação técnica:**

- [ ] Instrumentação (`web-vitals`, GA4) implementada e validada em ambiente de teste.
- [ ] Configuração do GA4 concluída (eventos, conversões, segmentos).
- [ ] Scripts ETL preparados e testados com dados de exemplo.
- [ ] Acesso a ambientes (teste/produção) confirmado e funcional.
- [ ] Piloto executado e ajustes implementados.
- [ ] Checklist de instrumentação validado.

**Documentação:**

- [ ] Plano experimental finalizado e aprovado (versão estável).
- [ ] Protocolo de ética aprovado e arquivado.
- [ ] Política de privacidade publicada (se aplicável).
- [ ] Termo de consentimento informado preparado (para laboratório, se aplicável).
- [ ] Guia de operação e dicionário de métricas disponíveis.

**Recursos e infraestrutura:**

- [ ] Acesso a ferramentas confirmado (GA4, BigQuery, CrUX, Lighthouse).
- [ ] Repositório Git configurado e documentação versionada.
- [ ] Ambiente de coleta disponível e estável.

**Comunicação:**

- [ ] Stakeholders informados sobre início da coleta (data, duração, expectativas).
- [ ] Canais de comunicação estabelecidos.

### 20.2 Aprovações finais para iniciar a operação

**Aprovações obrigatórias:**

1. **Comitê de Ética (CEP)**: Aprovação formal do protocolo (documento de aprovação arquivado).
2. **Orientador**: Aprovação acadêmica e metodológica para início da execução.
3. **Pesquisador Principal (PI)**: Confirmação de que todos os itens do checklist (20.1) estão completos.

**Aprovações recomendadas (go/no-go):**

4. **Stakeholders principais** (Produto, Dev Front-End, QA, Gestão): Validação de que objetivos e escopo estão alinhados; aprovação para prosseguir.

**Processo de registro:**

- **Formato**: E-mail formal ou documento assinado registrando aprovações.
- **Conteúdo**: Data, aprovadores, condições (se houver), assinatura/confirmação.
- **Arquivamento**: Documento de aprovação final arquivado no repositório (`/docs/aprovacoes/aprovacao-execucao-YYYY-MM-DD.md`).

**Critério de bloqueio:**

- **Nenhuma coleta de dados pode iniciar sem aprovação do CEP e do orientador.**
- **Recomenda-se aguardar go/no-go dos stakeholders, mas não é bloqueante se objetivos estiverem claros e alinhados.**

**Template de registro de aprovação:**

```markdown
# Aprovação para Início da Execução do Experimento

**Experimento**: CWV-BC-EXP-2025-001  
**Data**: [YYYY-MM-DD]

## Aprovações Obtidas

- [ ] Comitê de Ética (CEP): [Data] - [Número do protocolo]
- [ ] Orientador: [Nome] - [Data]
- [ ] Stakeholders: [Nomes/Cargos] - [Data]

## Condições e Observações

[Qualquer condição ou observação relevante]

## Assinaturas/Confirmações

- Pesquisador Principal: [Nome] - [Data]
```

---
