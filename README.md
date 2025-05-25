# План анализа системных промтов AI-ассистентов

Этот документ описывает предлагаемый порядок и структуру для анализа собранных системных промтов различных AI-ассистентов. Цель — извлечь лучшие практики, понять общие паттерны и специфические подходы к промт-инжинирингу для создания эффективных AI-агентов.

## Общий подход к анализу каждого промта:

Для каждого AI-ассистента / промта мы будем:
1.  **Определять идентичность и назначение:** Какова заявленная роль AI, для какой платформы или задачи он предназначен?
2.  **Анализировать структуру промта:** Выделять ключевые секции (например, инструкции по общению, правила вызова инструментов, обработка ошибок, специфичные для домена знания).
3.  **Изучать механизм взаимодействия с инструментами (Tools/Functions/MDX Components):** Как AI получает инструкции по вызову внешних функций? Какой формат используется (JSON, XML, кастомные теги)?
4.  **Выявлять специфические ограничения и возможности:** Какие правила наложены на AI (например, по безопасности, стилю кода, работе с файлами)? Какие уникальные возможности предоставляет система?
5.  **Отмечать интересные техники промт-инжиниринга:** Использование RAG, Chain-of-Thought, Few-shot learning, динамическая генерация промта, политики поведения и т.д.
6.  **Сравнивать с другими промтами:** Находить общие черты и различия в подходах.

## Порядок рассмотрения промтов:

Предлагается следующий порядок, сгруппированный по типам систем или их сложности/детализации. Это поможет нам постепенно наращивать понимание.

### Часть 1: AI-ассистенты для разработки в IDE и специализированных средах

Эти системы обычно тесно интегрированы со средой разработки и имеют специфический набор инструментов для взаимодействия с кодовой базой и файловой системой.

1.  **Lovable (`Lovable/Prompt.txt`)**
    *   Начнем с него, так как это был первый промт, который мы подробно разбирали. Он задает хороший базовый уровень понимания.
    *   **Фокус:** Веб-разработка (React), real-time изменения, кастомные XML-подобные команды.

2.  **Cursor Prompts**
    *   **`Cursor Prompts/Chat Prompt.txt` (GPT-4o)**
    *   **`Cursor Prompts/Agent Prompt.txt` (Claude 3.7 Sonnet)**
    *   **Фокус:** IDE-ассистент, сравнение подходов для разных LLM, "apply model", JSON-инструменты.

3.  **Codex CLI (`Open Source prompts/Codex CLI/Prompt.txt`)**
    *   **Фокус:** Терминальный агент от OpenAI, работа с локальной кодовой базой, `apply_patch` (diff-формат), git-контекст.

4.  **Cline / RooCode (`Open Source prompts/Cline/Prompt.txt` и `Open Source prompts/RooCode/Prompt.txt`)**
    *   (Предполагаем, что это связанные системы, возможно, RooCode – это UI-конфигурация для Cline)
    *   **Фокус:** XML-инструменты, режимы PLAN/ACT, MCP (Model Context Protocol), пользовательская кастомизация правил.

5.  **Bolt (`Open Source prompts/Bolt/Prompt.txt`)**
    *   **Фокус:** Работа в WebContainer, строгие ограничения среды (нет pip, C++, Git, diff/patch), динамическая генерация промта, Supabase, система "артефактов" (`<boltArtifact>`).

6.  **Same.new IDE (`Devin AI/Prompt.txt` - предполагаю, что это относится к Same.new, как мы обсуждали ранее) - *Уточнение: Если "Devin AI" – это отдельная сущность, мы рассмотрим ее как таковую. Если это кодовое имя для ассистента Same.new, то так и укажем.* **
    *   **Фокус:** Облачная IDE, веб-разработка (Bun, shadcn/ui), клонирование UI, версионирование, деплой (Netlify).

### Часть 2: AI-ассистенты для платформ и общего назначения

Эти системы могут быть как узкоспециализированными для своей платформы, так и предлагать более широкий спектр возможностей.

7.  **Vercel v0 (`v0 Prompts and Tools/`)**
    *   **`Prompt.txt`**
    *   **`Model.md`** (вероятно, описание модели или MDX-компонентов)
    *   **Фокус:** Платформа Vercel, Next.js App Router, **MDX как основной формат вывода и взаимодействия**, RAG, AI SDK от Vercel, цитирование источников.

8.  **Dia (`dia/Prompt.txt`)**
    *   **Фокус:** AI-ассистент для браузера Dia, уникальные фичи ("Ask Dia Hyperlinks", "Simple Answers"), строгие правила по медиа и LaTeX, классификация данных (trusted/untrusted).

9.  **Manus AI Assistant (`Manus Agent Tools & Prompt/`)**
    *   **`Prompt.txt`**
    *   **`Agent loop.txt`**
    *   **`Modules.txt`**
    *   **`tools.json`**
    *   **Фокус:** Сложная агентная архитектура (Planner, Knowledge, Datasource), цикл работы агента, вызов API данных через Python, строгие правила коммуникации и написания текстов.

### Часть 3: Конфигурации и вспомогательные файлы

10. **`docker-compose.txt`** (из нашей текущей сессии)
    *   Рассмотрим его как пример конфигурации инфраструктуры для поддержки AI-агентов (Traefik, Cloudflare Tunnel, n8n, Supabase).
    *   Обсудим, как принципы из промтов могут влиять на проектирование такой инфраструктуры.

---

# **FULL v0, Cursor, Manus, Same.dev, Lovable, Devin, Replit Agent, Windsurf Agent, VSCode Agent, Dia Browser & Trae AI (And other Open Sourced) System Prompts, Tools & AI Models**  

(All the published system prompts are extracted by myself, except the already open sourced ones, Manus and Dia, which are contributions)

🚀 **I managed to obtain FULL official v0, Manus, Cursor, Same.dev, Lovable, Devin, Replit Agent, Windsurf Agent, VSCode Agent, Dia browser & Trae AI system prompts and internal tools.**

📜 Over **7000+ lines** of insights into their structure and functionality.  

## 📂 **Available Files**
- **v0 Folder**  
- **Manus Folder**
- **Lovable Folder**
- **Devin Folder**
- **Same.dev Folder**
- **Replit Folder**
- **Windsurf Agent Folder**
- **VSCode (Copilot) Agent Folder**
- **Cursor Folder**
- **Dia Folder**
- **Trae AI Folder**
- **Open Source prompts Folder**
  - Codex CLI
  - Cline
  - Bolt
  - RooCode

---

## 🗓️ **Zero Calendar (my new project)**

**An Open-Source AI-Powered Calendar for the Future of Scheduling**

Zero Calendar is an open-source AI calendar solution that gives users the power to manage their schedule intelligently while integrating with external services like Google Calendar and other calendar providers. Our goal is to modernize and improve scheduling through AI agents to truly revolutionize how we manage our time.

For more details, check out the [Zero Calendar repository](https://github.com/Zero-Calendar/zero-calendar).

---

## 🛠 **Roadmap & Feedback**

🚨 **Note:** We no longer use GitHub issues for roadmap and feedback.  
Please visit [System Prompts Roadmap & Feedback](https://systemprompts.featurebase.app/) to share your suggestions and track upcoming features.

🆕 **LATEST UPDATE:** 15/05/2025 

## ❤️ Support the Project

If you find this collection valuable and appreciate the effort involved in obtaining and sharing these insights, please consider supporting the project. Your contribution helps keep this resource updated and allows for further exploration.


## 🔗 **Connect With Me**  
✖ **X:** [NotLucknite](https://x.com/NotLucknite)  
💬 **Discord:** `x1xh`  

## 🛡️ **Security Notice for AI Startups***

⚠️ **If you're an AI startup, make sure your data is secure.** Exposed prompts or AI models can easily become a target for hackers.

🔐 **Interested in securing your AI systems?**  
Check out **[ZeroLeaks](https://0leaks.vercel.app)**, a service designed to help startups **identify and secure** leaks in system instructions, internal tools, and model configurations. **Get a free AI security audit** to ensure your AI is protected from vulnerabilities.


**The company is mine, this is NOT a 3rd party AD.*

## 📊 **Star History**

<a href="https://www.star-history.com/#x1xhlol/system-prompts-and-models-of-ai-tools&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=x1xhlol/system-prompts-and-models-of-ai-tools&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=x1xhlol/system-prompts-and-models-of-ai-tools&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=x1xhlol/system-prompts-and-models-of-ai-tools&type=Date" />
 </picture>
</a>

⭐ **Drop a star if you find this useful!**
