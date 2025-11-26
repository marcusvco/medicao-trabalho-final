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
