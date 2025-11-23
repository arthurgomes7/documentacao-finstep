# 🚀 FinStep - Plataforma de Educação Financeira Gamificada com IA

> **Transformando o aprendizado sobre investimentos em uma jornada prática, interativa e personalizada.**

![Status](https://img.shields.io/badge/Status-Em_Desenvolvimento-yellow)
![Backend](https://img.shields.io/badge/Backend-Python_3.12%2B-blue)
![Frontend](https://img.shields.io/badge/Frontend-React_18%2B-cyan)
![AI](https://img.shields.io/badge/AI-Google_Gemini-orange)
![Database](https://img.shields.io/badge/DB-PostgreSQL%2FSQLAlchemy-informational)

---

## 📖 1. Contexto e Objetivo

A educação financeira é uma competência essencial, mas muitas vezes negligenciada ou considerada monótona.A falta de conhecimento prático leva a decisões ruins e perda de oportunidades.

O **FinStep** resolve isso combinando **LMS (Learning Management System)** com **Gamificação** e **Inteligência Artificial**. [cite_start]O objetivo é desenvolver uma plataforma web onde o usuário aprende através de trilhas interativas e aplica o conhecimento em um simulador de investimentos em tempo real, com o suporte de um "tutor financeiro" baseado em IA [cite: 361-364].

---

## ✨ 2. Funcionalidades Principais

### 🤖 Assistente Inteligente (IA)
* [cite_start]**Tutor 24/7:** Chatbot integrado (`AIChat.tsx`) que utiliza a API do **Google Gemini**[cite: 430].
* **Respostas Contextuais:** Tira dúvidas sobre aulas e termos técnicos sem sair da tela.
* [cite_start]**RAG (Retrieval-Augmented Generation):** A IA acessa o `investor_profile` do usuário para personalizar conselhos (ex: alertar perfis conservadores sobre riscos de cripto)[cite: 502].

### 🗺️ Trilha de Aprendizado (LMS)
* [cite_start]**Jornada Visual:** Mapa de progresso (`LearningPath.tsx`) com nós de lições sequenciais [cite: 433-434].
* [cite_start]**Mecânica de Desbloqueio:** Lições concluídas ficam verdes, a atual desbloqueada e futuras bloqueadas (cadeado) [cite: 435-436].
* **Quizzes:** Validação de conhecimento ao final de cada módulo.

### 📈 Módulo de Investimentos (Simulador)
* [cite_start]**Home Broker Simulado:** Painel (`Investimentos.tsx`) para compra e venda de Ações, FIIs e Criptoativos com dinheiro fictício [cite: 438-439].
* [cite_start]**Análise de Ativos:** Visualização de gráficos e fundamentos de mercado (`InvestmentView.tsx`)[cite: 440].

### 🎮 Gamificação e Engajamento
* [cite_start]**Sistema de Ligas:** Usuários competem em rankings semanais (`Leaderboard.tsx`) baseados em XP[cite: 388, 514].
* [cite_start]**Missões Diárias:** Desafios curtos (ex: "Ganhe 10 XP") para incentivar o login diário (`DailyMissions.tsx`)[cite: 443].
* **Conquistas:** Medalhas desbloqueáveis por marcos alcançados.

### 💰 Gestão Financeira Pessoal
* [cite_start]Registro e categorização de despesas reais (`Expenses.tsx`), conectando a teoria de investimentos com a realidade do orçamento doméstico [cite: 445-448].

---

## 🏗️ 3. Arquitetura da Solução

O sistema segue uma arquitetura **Cliente-Servidor RESTful**:

1.  **Frontend (SPA):** React.js gerenciando a interface e estado.
2.  **Backend (API):** Flask (Python) processando regras de negócio e integrações.
3.  **Banco de Dados:** Relacional (SQLAlchemy) garantindo integridade transacional.
4.  **IA Externa:** Integração com Google Gemini via API.

### Fluxo de Dados (IA)
1.  Usuário envia pergunta no Chat.
2.  Backend recebe, busca contexto do usuário (RAG) e injeta "System Prompt".
3.  Google Gemini processa e retorna a resposta didática.
4.  [cite_start]Resposta é salva em `ai_chat_logs` e enviada ao Frontend [cite: 499-502].

---

## 📂 4. Estrutura do Projeto

### 4.1. Frontend (`/frontend`)
[cite_start]Arquitetura modular baseada em componentes funcionais e TypeScript [cite: 453-482].

```text
frontend/
├── node_modules/         # Dependências
├── src/
│   ├── components/
│   │   ├── figma/        # Assets de design
│   │   └── ui/           # Biblioteca de Componentes Visuais
│   │       ├── AIChat.tsx               # Interface do Chatbot
│   │       ├── DailyMissions.tsx        # Widget de Missões
│   │       ├── Expenses.tsx             # Gestão de Gastos
│   │       ├── Home.tsx                 # Dashboard Principal
│   │       ├── Investments.tsx          # Home Broker Simulado
│   │       ├── InvestmentView.tsx       # Detalhes do Ativo
│   │       ├── Leaderboard.tsx          # Ranking da Liga
│   │       ├── LearningPath.tsx         # Mapa da Trilha
│   │       ├── LessonModal.tsx          # Aula e Quiz
│   │       ├── Login.tsx                # Autenticação
│   │       ├── Onboarding.tsx           # Fluxo Inicial
│   │       ├── PathSelection.tsx        # Escolha de Trilhas
│   │       ├── Profile.tsx              # Perfil do Usuário
│   │       ├── Sidebar.tsx              # Navegação Lateral
│   │       └── XPProgress.tsx           # HUD (Nível/XP)
│   ├── guidelines/       # Diretrizes de UI/UX
│   ├── styles/           # Tailwind e CSS Global
│   └── App.tsx           # Componente Raiz (Rotas)
```
### 🛠️ Tecnologias Principais

Utilizamos uma stack moderna focada em performance e experiência de desenvolvimento:

* ![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB) **React.js 18+**: Para construção da interface de usuário reativa e baseada em componentes.
* ![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=flat&logo=typescript&logoColor=white) **TypeScript**: Garante segurança de código através de tipagem estática em interfaces.
* ![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white) **Tailwind CSS**: Framework utilitário para estilização rápida e responsiva.
* **react-icons**: Biblioteca para implementação de ícones consistentes (ex: `FaTimes`, `FaPaperPlane`, `FaRobot`).
![Texto alternativo](trilha-principal.jpeg)

### 4.2. Backend (`/backend`)
[cite_start]Padrão *Application Factory* para escalabilidade e testes [cite: 486-497].

```text
backend/
├── app/
│   ├── api/              # Blueprints (Rotas)
│   │   ├── __init__.py
│   │   ├── auth.py       # Login/Signup
│   │   ├── education.py  # Lições e Trilhas
│   │   └── routes.py     # Rotas Gerais
│   ├── core/             # Configs (Env, Extensions)
│   ├── database/         # Sessão do DB
│   ├── models/           # Modelos ORM (SQLAlchemy)
│   ├── services/         # Lógica de Negócio
│   │   └── rag_engine.py # Motor de IA (Integração Gemini)
│   └── __init__.py       # Create_app Factory
├── tests/                # Testes Automatizados (Pytest)
│   ├── conftest.py
│   └── test_api.py
├── .env                  # Variáveis de Ambiente
├── pyproject.toml        # Dependências
└── run.py                # Entrypoint do Servidor
