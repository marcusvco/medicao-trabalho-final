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
