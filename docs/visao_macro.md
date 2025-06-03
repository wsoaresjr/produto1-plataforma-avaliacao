# Visão Macro
# Produto 1 – Plataforma de Avaliação Híbrida

> *Versão inicial – 4 de junho de 2025*

---

## 1  Propósito / Problema

A perspectiva é que a plataforma de avaliação híbrida seja uma ferramenta bastante útil para ajudar os profissionais da educação (professores, coordenadores pedagógicos e diretores escolares) a identificarem com mais precisão o desenvolvimento dos estudantes nas mais variadas habilidades previstas na BNCC.

Ela é necessária pois torna útil o processo de confecção de uma avaliação (para ser aplicada de forma impressa ou online).

---

## 2  Público‑alvo / Personas

**Alunos**  \– basicamente realizarão as provas. No entanto, a expectativa é que possam acompanhar o próprio desenvolvimento ao longo do tempo.

**Professores**  \– responsáveis por criar as avaliações impressas ou on‑line. Poderão:

* filtrar itens pela BNCC e metadados;
* visualizar metadados e conteúdo do item;
* marcar (checkbox) os itens selecionados;
* gerar PDF da prova completa e dos cartões‑resposta individualizados;
* ou publicar a prova diretamente para a turma/aluno (modo on‑line);
* lançar respostas on‑line automaticamente ou digitar cartões‑resposta digitalizados;
* acessar dashboards de turma/aluno após a correção.

**Coordenadores Pedagógicos / Diretores**  \– acessarão dashboards consolidados da escola, com drill‑down por segmento, turma e aluno.

O fluxo de login direciona cada perfil às telas adequadas.

---

## 3  Proposta de Valor

* Personalização da experiência de uso de acordo com o perfil (aluno, professor, gestor).
* Correção rápida (on‑line ou por leitura de cartões) reduzindo carga administrativa.
* Banco de itens alinhado à BNCC com filtros inteligentes.
* Futuro acompanhamento individual do estudante, tornando‑o agente de seu próprio desenvolvimento.

---

## 4  Escopo do **MVP** (Junho 2025)

| Módulo                      | Funcionalidades mínimas                                                                                                                                  |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Banco de Itens**          |  • Cadastro/curadoria de itens alinhados à BNCC<br>• Filtros por disciplina, habilidade, dificuldade                                                     |
| **Composição de Provas**    |  • Seleção múltipla de itens<br>• Ordenação e paginação<br>• Geração de prova **PDF** e cartões‑resposta PDF individualizados                            |
| **Provas On‑line**          |  • Agendamento e atribuição por turma/aluno<br>• Interface responsiva para alunos<br>• Salvamento automático de respostas                                |
| **Correção & Resultados**   |  • Importação automática das respostas on‑line<br>• Tela de digitação de cartões impressos<br>• Cálculo de acertos, porcentual, pontuação por habilidade |
| **Dashboards do Professor** |  • Visão turma → aluno<br>• Download de relatórios CSV/PDF                                                                                               |
| **Autenticação & Perfis**   |  • Grupos: Aluno, Professor, Coordenação/Direção<br>• Redirecionamento a dashboards específicos                                                          |

---

## 5  Roadmap **Pós‑MVP** (Q3 – Q4 / 2025)

* Testes adaptativos (IA) \– seleção dinâmica de itens.
* Analytics avançado (machine learning) \– previsão de desempenho e alertas precoces.
* App mobile para alunos (Android/iOS).
* Integração com LMS (Google Classroom, Moodle).
* Gamificação e recomendações personalizadas de estudo.
* API pública para parceiros e integrações estaduais.

---

## 6  Arquitetura de Alto Nível

* **Frontend SPA:** React + Material UI (ou equivalente) servido por CDN.
* **Backend API:** Python ( FastAPI ) em contêineres Docker.
* **Banco relacional:** PostgreSQL (read replicas para escalabilidade).
* **OCR Service:** micro‑serviço em Python com Tesseract para leitura de cartões.
* **Armazenamento de arquivos:** S3 compatível (minio / AWS S3).
* **Autenticação:** OAuth 2.0 / JWT; provisionamento SSO (Google, Microsoft).
* **CI/CD:** GitHub Actions → Docker Registry → Kubernetes (Helm charts).
* **Observabilidade:** Prometheus + Grafana; logs estruturados (ELK).

*(Diagrama em desenvolvimento – inserir Mermaid posteriormente)*

---

## 7  Integrações Externas

| Integração                       | Objetivo                                             |
| -------------------------------- | ---------------------------------------------------- |
| **Base de Dados Eureka**         | Importar habilidades, descritores e itens existentes |
| **Serviço de E‑mail (SendGrid)** | Notificações de prova publicada e relatórios         |
| **OCR / Vision API**             | Alternativa à engine local para maior acurácia       |
| **SSO Institucional**            | Login único via Google Workspace ou Microsoft Entra  |
| **Analytics (Matomo)**           | Métricas de uso e funil de navegação                 |

---

## 8  Requisitos Não‑Funcionais

* **Escalabilidade:** suportar ≥10 000 alunos simultâneos durante pico de aplicação de provas.
* **Disponibilidade:** ≥99,5 % SLA mensal.
* **Performance:** resposta API < 500 ms (p95); correção completa < 2 min por prova.
* **LGPD:** dados pessoais criptografados em repouso (AES‑256) e em trânsito (TLS 1.3);
  contratos de operador x controlador.
* **Acessibilidade:** WCAG 2.1 AA.
* **Segurança:** OWASP Top 10; testes de penetração semestrais.

---

## 9  Métricas de Sucesso

* ≥70 % dos professores da rede criando ao menos 1 avaliação no semestre.
* Tempo médio de criação de avaliação ≤ 50 min.
* Tempo médio de correção (impressa) ≤ 15 min após upload dos cartões.
* NPS ≥ 65 entre professores.
* Redução de 90 % nos erros de correção manual.
* Engajamento dos alunos: ≥ 80 % concluem as provas on‑line no prazo.

---

## 10  Stakeholders & Papéis

| Papel                        | Responsável                              | Descrição                          |
| ---------------------------- | ---------------------------------------- | ---------------------------------- |
| **Product Owner**            |  Consultor (Squad Pedagógico)            | Prioriza backlog e valida entregas |
| **Tech Lead**                |  \[Nome]                                 | Arquitetura, revisão de código     |
| **Desenvolvedores**          | 2–3 full‑stack                           | Implementação, testes              |
| **UX Designer**              |  \[Nome]                                 | Jornada do usuário e protótipos    |
| **Equipe Pedagógica Eureka** | Conteúdo de itens e validação BNCC       |                                    |
| **TI Cliente**               | Infra local, SSO, políticas de segurança |                                    |
| **Patrocinador**             |  Secretaria de Educação                  | Aprovação de orçamento e metas     |

---

## 11  Riscos & Mitigações

| Risco                          | Impacto                | Prob. | Mitigação                                                |
| ------------------------------ | ---------------------- | ----- | -------------------------------------------------------- |
| Atraso na curadoria de itens   | MVP incompleto         | Médio | Sprint dedicado + curadores externos                     |
| Baixa acurácia do OCR          | Correções imprecisas   | Alto  | Piloto + fallback digitação manual + ajuste de contraste |
| Adoção baixa pelos professores | Subutilização          | Médio | Programa de formação + suporte in‑app                    |
| Escalonamento de infra         | Instabilidade em picos | Baixo | Kubernetes HPA + testes de carga                         |
| Conformidade LGPD              | Multas / imagem        | Baixo | DPO, auditoria externa semestral                         |

---

*Esta visão macro é um documento vivo e será atualizada continuamente conforme novas decisões de produto e arquitetura forem registradas.*
