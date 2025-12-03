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
