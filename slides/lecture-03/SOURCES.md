# Верификация фактов занятия 3

Слайды — `lecture-03.md` (48 слайдов) в этом каталоге. Структура вечера и реплики лектора —
`teacher/meeting-03-outline.md`; коды источников совпадают с его таблицей «Источники».

Формат тот же, что у лекций 1 и 2: каждое утверждение с цифрой, именем или цитатой сверено
с источником. Все ссылки открыты и проверены **24 сентября 2026**, новые TOT и PS — **27 сентября 2026**; у документации вендоров
даты публикации нет — указана дата обращения. **КУРС** — методическое решение или вывод курса,
а не факт из источника.

| Код | Источник | URL |
|---|---|---|
| **COT** | Wei et al. Chain-of-Thought Prompting Elicits Reasoning in Large Language Models, 28.01.2022 | https://arxiv.org/abs/2201.11903 |
| **ZS** | Kojima et al. Large Language Models are Zero-Shot Reasoners, 24.05.2022 | https://arxiv.org/abs/2205.11916 |
| **REACT** | Yao et al. ReAct: Synergizing Reasoning and Acting in Language Models, 06.10.2022 | https://arxiv.org/abs/2210.03629 |
| **REFL** | Shinn et al. Reflexion: Language Agents with Verbal Reinforcement Learning, 20.03.2023 | https://arxiv.org/abs/2303.11366 |
| **SC** | Huang et al. Large Language Models Cannot Self-Correct Reasoning Yet, 03.10.2023 | https://arxiv.org/abs/2310.01798 |
| **TOT** | Yao et al. Tree of Thoughts: Deliberate Problem Solving with Large Language Models, 17.05.2023 | https://arxiv.org/abs/2305.10601 |
| **PS** | Wang et al. Plan-and-Solve Prompting: Improving Zero-Shot Chain-of-Thought Reasoning by Large Language Models, 06.05.2023 | https://arxiv.org/abs/2305.04091 |
| **THINK** | Claude Docs. Thinking: steering and cost (обр. 24.09.2026) | https://platform.claude.com/docs/en/build-with-claude/thinking-steering-and-cost |
| **OAI** | OpenAI. Reasoning models (обр. 24.09.2026) | https://developers.openai.com/api/docs/guides/reasoning |
| **BEA** | Anthropic. Building effective agents, 19.12.2024 | https://www.anthropic.com/engineering/building-effective-agents |
| **COALA** | Sumers, Yao, Narasimhan, Griffiths. Cognitive Architectures for Language Agents, 05.09.2023 | https://arxiv.org/abs/2309.02427 |
| **GENAG** | Park et al. Generative Agents: Interactive Simulacra of Human Behavior, 07.04.2023 | https://arxiv.org/abs/2304.03442 |
| **MEMGPT** | Packer et al. MemGPT: Towards LLMs as Operating Systems, 12.10.2023 | https://arxiv.org/abs/2310.08560 |
| **WENG** | Lilian Weng. LLM Powered Autonomous Agents, 23.06.2023 | https://lilianweng.github.io/posts/2023-06-23-agent/ |
| **LITM** | Liu et al. Lost in the Middle: How Language Models Use Long Contexts, 06.07.2023 | https://arxiv.org/abs/2307.03172 |
| **ROT** | Chroma. Context Rot: How Increasing Input Tokens Impacts LLM Performance, 14.07.2025 | https://www.trychroma.com/research/context-rot |
| **CTX** | Anthropic. Effective context engineering for AI agents, 29.09.2025 | https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents |
| **CACHE** | Claude Docs. Prompt caching (обр. 24.09.2026) | https://platform.claude.com/docs/en/build-with-claude/prompt-caching |
| **MEMT** | Claude Docs. Memory tool (обр. 24.09.2026) | https://platform.claude.com/docs/en/agents-and-tools/tool-use/memory-tool |
| **CCM** | Claude Code Docs. How Claude remembers your project (обр. 24.09.2026) | https://code.claude.com/docs/en/memory |
| **MCP1** | Model Context Protocol. What is MCP (обр. 24.09.2026) | https://modelcontextprotocol.io/docs/getting-started/intro |
| **MCPT** | MCP Specification 2026-07-28, Server / Tools | https://modelcontextprotocol.io/specification/2026-07-28/server/tools |
| **MCPS** | MCP Specification 2026-07-28, Transports / stdio | https://modelcontextprotocol.io/specification/2026-07-28/basic/transports/stdio |
| **PYSDK** | MCP Python SDK. Migration Guide v1 → v2; PyPI `mcp` 2.2.0 от 07.09.2026 | https://py.sdk.modelcontextprotocol.io/v2/migration/ · https://pypi.org/project/mcp/ |
| **INJ** | Greshake et al. Not what you've signed up for: … Indirect Prompt Injection, 23.02.2023 | https://arxiv.org/abs/2302.12173 |
| **КУРС** | `notebooks/02_tool_calling_agent.ipynb`, `notebooks/data/agent_facts.json`, `teacher/meeting-03-outline.md`, лекция 2 | в репозитории |

---

## Часть 1. Вводная лекция

| Слайд | Утверждение | Что в источнике | Ист. |
|---|---|---|---|
| 3 | Тезис: четыре места цикла — рассуждение, инструмент, контекст, память; MCP меняет только источник инструмента | выведено из механики цикла практики 2 и определения MCP (MCP1) | КУРС |
| 5 | Карта лекции: четыре блока — четыре места цикла `run_agent` | нарисована для курса по циклу практики 2 | КУРС |
| 7 | MCP — открытый стандарт подключения ИИ-приложений к внешним системам | «MCP (Model Context Protocol) is an open-source standard for connecting AI applications to external systems» | MCP1 |
| 8 | Разрез «где живёт»: процесс, автор docstring, вызов по имени / через `tools/call` | таблица «Инструмент против MCP-сервера» лекции 2; `tools/call` — MCP «Architecture overview» | КУРС, MCP1 |
| 8 | Разрез «как узнают»: `TOOLS` руками / `tools/list` в рантайме | там же; `tools/list` — MCP «Architecture overview» | КУРС, MCP1 |
| 8 | Разрез «что контролируете»: описание чужое, ошибка по контракту `isError`, объём чужой | `isError` — MCPT; остальное — вывод курса | MCPT, КУРС |
| 8 | Модель видит ровно то же: имя, описание, схему | таблица лекции 2, строка «Что видит модель» | КУРС |
| 9 | Схема «хост, клиент, сервер» | та же схема, что на лекции 2 (`slides/lecture-02/assets/mcp-host-client-server.svg`), сверена там | КУРС |
| 11 | Промежуточные шаги улучшают арифметику, здравый смысл, символьные задачи | «chain of thought prompting improves performance on a range of arithmetic, commonsense, and symbolic reasoning tasks» | COT |
| 11 | Хватает фразы «давайте подумаем шаг за шагом» | «LLMs are decent zero-shot reasoners by simply adding "Let's think step by step" before each answer» | ZS |
| 12 | ReAct чередует мысль и действие | «generate both reasoning traces and task-specific actions in an interleaved manner» | REACT |
| 13 | Tree of Thoughts: несколько мыслей на шаг, оценка, выбор, откат | «allows LMs to perform deliberate decision making by considering multiple different reasoning paths and self-evaluating choices to decide the next course of action, as well as looking ahead or backtracking when necessary to make global choices» | TOT |
| 13 | Plan-and-Solve: сначала план из подзадач, потом выполнение по плану | «first, devising a plan to divide the entire task into smaller subtasks, and then carrying out the subtasks according to the plan» | PS |
| 13 | Reflexion: вывод после неудачи — в память, читается в следующей попытке | см. слайд 16 | REFL |
| 13 | Reasoning-модели: встроено, не показывается, оплачивается, занимает окно | см. слайд 18 | THINK, OAI |
| 13 | Три ветки — из chain-of-thought, одна — из ReAct | ToT и PS строятся на CoT (по текстам статей: ToT «generalizes over the popular Chain of Thought approach», PS — «zero-shot chain-of-thought»); Reflexion — на ReAct (агент ReAct как базовый в статье); reasoning-модели — рассуждение внутри модели. «К циклу» подписи — вывод курса | TOT, PS, REFL, КУРС |
| 14 | ToT: на каждом шаге несколько мыслей, оценка, выбор, откат; рис. 1 (c) против (d) | «allows LMs to perform deliberate decision making by considering multiple different reasoning paths and self-evaluating choices to decide the next course of action, as well as looking ahead or backtracking when necessary to make global choices» | TOT |
| 14 | Игра 24: GPT-4 с chain-of-thought — 4 %, с ToT — 74 % | «in Game of 24, while GPT-4 with chain-of-thought prompting only solved 4% of tasks, our method achieved a success rate of 74%» (аннотация) | TOT |
| 14 | Зелёные ветки рис. 1 — выбранные, розовые — отброшенные; «в цикле агента» — сравнение вариантов до вызова | по цветам рисунка 1 (d); вторая часть — вывод курса | TOT, КУРС |
| 15 | Plan-and-Solve: план из подзадач, потом выполнение по плану | «first, devising a plan to divide the entire task into smaller subtasks, and then carrying out the subtasks according to the plan» | PS |
| 15 | Пример рис. 2: (a) Zero-shot-CoT — 55 %, неверно; (b) PS — 12/20 = 60 %, верно | рисунок 2 статьи, GPT-3 | PS |
| 15 | PS направлен на ошибку «пропущен шаг» | «To address the missing-step errors, we propose Plan-and-Solve (PS) Prompting» | PS |
| 16 | Reflexion: разбор обратной связи, вывод в память, учёт в следующей попытке | «Reflexion agents verbally reflect on task feedback signals, then maintain their own reflective text in an episodic memory buffer to induce better decision-making in subsequent trials» | REFL |
| 16 | Без внешней обратной связи самокоррекция плохая, иногда хуже | «LLMs struggle to self-correct their responses without external feedback, and at times, their performance even degrades after self-correction» | SC |
| 16 | Внешняя обратная связь агента — результат инструмента, текст ошибки из TODO 2 | вывод курса: TODO 2 практики 2 возвращает ошибку строкой | КУРС |
| 17 | Reflexion, рис. 1: попытка → оценка → словесная рефлексия → следующая попытка; три задачи | рисунок 1 статьи (decision making, programming, reasoning); цитата та же, что на слайде 19 | REFL |
| 18 | Рассуждение оплачивается как выходные токены | «Tokens Claude uses while thinking (billed as output tokens)» | THINK |
| 18 | …и занимает место в контексте | «While reasoning tokens are not visible via the API, they still occupy space in the model's context window and are billed as output tokens» | OAI |
| 18 | Платить за рассуждение, когда задача многошаговая | правило курса | КУРС |
| 19 | Рассуждение не гарантирует точного числа; число считает инструмент | вывод курса; не утверждается, что CoT не помогает в арифметике — по COT помогает | КУРС |
| 21 | Базовый блок — модель + поиск, инструменты, память | «The basic building block of agentic systems is an LLM enhanced with augmentations such as retrieval, tools, and memory» | BEA |
| 22 | Рабочая память — контекст текущего шага | «Working memory maintains active and readily available information as symbolic variables for the current decision cycle» | COALA |
| 22 | Эпизодическая — опыт прошлых шагов | «Episodic memory stores experience from earlier decision cycles» | COALA |
| 22 | Семантическая — знания о мире и о себе | «Semantic memory stores an agent's knowledge about the world and itself» | COALA |
| 22 | Процедурная: неявно — веса, явно — код агента | «Language agents contain two forms of procedural memory: implicit knowledge stored in the LLM weights, and explicit knowledge written in the agent's code» | COALA |
| 22 | Долговременная — внешнее хранилище и поиск | «the capability to retain and recall (infinite) information over extended periods, often by leveraging an external vector store and fast retrieval» (в outline) | WENG |
| 23 | Memory tool: модель просит операцию, приложение выполняет и хранит | «The memory tool operates client-side: Claude requests file operations, and your application executes them» | MEMT |
| 23 | Generative Agents: журнал опыта, рефлексии, извлечение при планировании | «store a complete record of the agent's experiences using natural language, synthesize those memories over time into higher-level reflections, and retrieve them dynamically to plan behavior» | GENAG |
| 24 | Память как два инструмента `remember` / `recall` на том же MCP-сервере, файл на стороне сервера; это TODO 2 | решение курса; у Anthropic хранилище на стороне приложения (MEMT), на слайде это оговорено; эталон практики 3 прогнан 28.09.2026 | КУРС, MEMT |
| 27 | Вызов 1: system + user; вызов 2: плюс вызов и результат 9 761 | прогон эталона практики 2: 2 итерации, 1 вызов; 9 761 — `unload_lsn_2021_03` в `agent_facts.json`. Третья колонка подписана на схеме как иллюстрация | КУРС |
| 28 | Контекст — ограниченный ресурс с убывающей отдачей | «context, therefore, must be treated as a finite resource with diminishing marginal returns» | CTX |
| 28 | Деградация с ростом входа, неравномерная | «model performance degrades as input length increases, often in surprising and non-uniform ways» | ROT |
| 28 | Результат инструмента остаётся в списке и уходит заново на каждом вызове | механика `run_agent` практики 2 | КУРС |
| 29 | U-кривая: начало и конец лучше середины | «performance is often highest when relevant information occurs at the beginning or end of the input context, and significantly degrades when models must access relevant information in the middle of long contexts»; рисунок 1 статьи | LITM |
| 29 | В середине точность ниже, чем без документов (пунктир) | по рисунку 1: пунктир closed-book ≈ 56, точки 7–16 ниже него | LITM |
| 30 | Сжатие в сводку | «taking a conversation nearing the context window limit, summarizing its contents, and reinitiating a new context window with the summary» | CTX |
| 30 | Заметки вне контекста | «the agent regularly write notes persisted to memory outside of the context window» | CTX |
| 30 | Очистка результатов — самая безопасная форма сжатия | «one of the safest lightest touch forms of compaction» | CTX |
| 30 | MemGPT: контекст как оперативная память ОС | «virtual context management, a technique drawing inspiration from hierarchical memory systems in traditional operating systems» | MEMGPT |
| 30 | Кэширование снижает цену и задержку | «This significantly reduces processing time and costs for repetitive tasks or prompts with consistent elements» | CACHE |
| 30 | …но размер контекста не меняет | вывод курса: страница этого прямо не говорит | КУРС |
| 31 | Результат MCP-инструмента попадает в `messages` как есть; объём — чужой; клиент — последний рубеж | вывод курса из механики `call_tool` практики 3; очистка результатов — CTX (см. слайд 30) | КУРС, CTX |
| 32 | Мост: четыре TODO, у каждого «до» и «после» | ноутбук `notebooks/03_mcp_server_client.ipynb`; эталон прогнан на прокси 28.09.2026, `check()` 8/8 | КУРС |

## Часть 2. Практика

| Слайд | Утверждение | Что в источнике | Ист. |
|---|---|---|---|
| 34–37 | Артефакт, критерий 4/4 и 8/8, четыре TODO, форма «до / после», контрольные точки | `notebooks/03_mcp_server_client.ipynb` и `teacher/meeting-03-outline.md`; эталон прогнан 28.09.2026 | КУРС |
| 35 | В `mcp` 2.x `FastMCP` переименован в `MCPServer` | «The `FastMCP` class has been renamed to `MCPServer` to better reflect its role as the main server class in the SDK» | PYSDK |
| 36 | Лог печатает токены контекста и мысль модели на каждом шаге | `run_agent` ноутбука: `usage.prompt_tokens` и `msg.content` из ответа провайдера | КУРС |
| 38 | В stdout сервера — только сообщения MCP, логи — в stderr | «The server MUST NOT write anything to its stdout that is not a valid MCP message» · «The server MAY write UTF-8 strings to stderr for any logging purposes» | MCPS |
| 38 | На 2.2.0 `print` не рвёт вызов, но клиент печатает ошибку разбора JSON | прогон 24.09.2026: `ValidationError … Invalid JSON`, вызов вернул 9761 | КУРС |
| 38 | Удалённое `tool`-сообщение → ошибка 400 провайдера | требование формата chat completions: на каждый `tool_call_id` нужен ответ; в ноутбуке — `check()` 7 | КУРС |

## Часть 3. Итоги

| Слайд | Утверждение | Что в источнике | Ист. |
|---|---|---|---|
| 40 | Ошибка инструмента должна нести подсказку для исправления | см. слайд 47 | MCPT |
| 40 | `ToolError` — текст уходит модели; падение — текст остаётся на сервере | прогон 24.09.2026 и код SDK 2.2.0 (`mcp/server/mcpserver/tools/base.py`: «A crash: the exception's own text stays on the server») | PYSDK |
| 40 | Зачем: трейсбэк не должен утекать | вывод курса | КУРС |
| 41 | Claude Code подгружает память в начале каждого разговора | «Claude Code has two complementary memory systems. Both are loaded at the start of every conversation» | CCM |
| 41 | Memory tool: файлы, которые переживают сессию | «Claude can create, read, update, and delete files that persist between sessions» | MEMT |
| 42 | С ростом токенов модель хуже вспоминает | «as the number of tokens in the context window increases, the model's ability to accurately recall information from that context decreases» | CTX |
| 42 | Субагенты с чистым контекстом | «specialized sub-agents can handle focused tasks with clean context windows» | CTX |
| 43 | Описания инструментов недоверенного сервера — недоверенные | «For trust & safety and security, clients MUST consider tool annotations to be untrusted unless they come from trusted servers» | MCPT |
| 43 | Косвенная инъекция промпта: инструкции внутри данных | «We argue that LLM-Integrated Applications blur the line between data and instructions» | INJ |
| 42 | Очистку результатов студенты сделали в TODO 4 | ноутбук практики 3 | КУРС |
| 44–47 | Проект со свободной темой, идеи, вопросы, ДЗ (механика MCP, `ToolError`, `gu12`), дата 15 октября | решения курса: `syllabus.md`, `teacher/meeting-03-outline.md` | КУРС |
| 47 | `ToolError`: ошибка исполнения инструмента уходит модели с `isError: true`, чтобы она могла исправиться | «Tool Execution Errors contain actionable feedback that language models can use to self-correct and retry with adjusted parameters» · «They are reported in tool results with `isError: true`» | MCPT |

---

## Рисунки

| Файл | Слайд | Откуда |
|---|---|---|
| `assets/lecture-map.svg` | 5 | нарисован для курса; цикл — практика 2, четыре подписи — блоки лекции |
| `assets/mcp-host-client-server.svg` | 9 | копия схемы лекции 2 |
| `assets/reasoning-lineage.svg` | 13 | нарисован для курса; основа и ветки — COT, REACT, TOT, PS, REFL, THINK/OAI; подписи «к циклу» — курса |
| `assets/memory-types.svg` | 22 | нарисован для курса; деление памяти — COALA, примеры — данные курса |
| `assets/messages-growth.svg` | 27 | нарисован для курса; числа — `agent_facts.json` |
| `assets/lost-in-the-middle-fig1.png` | 29 | Liu et al., 2023, рис. 1, с. 1 arXiv v3; вырезан из PDF без изменений |
| `assets/tot-fig1.png` | 14 | Yao et al., 2023, рис. 1, с. 2 arXiv v2; вырезан из PDF без изменений |
| `assets/plan-and-solve-fig2.png` | 15 | Wang et al., 2023, рис. 2 (a), (b), с. 3 arXiv v3; вырезан из PDF, часть (c) не включена |
| `assets/reflexion-fig1.png` | 17 | Shinn et al., 2023, рис. 1, с. 3 arXiv v4; вырезан из PDF без изменений |

## Оговорки

1. **Спецификация MCP.** Актуальная версия — 2026-07-28. В ней протокол stateless, без рукопожатия
   `initialize`; `syllabus.md` (литература, п. 6) до сих пор ссылается на 2025-06-18. Для практики 3
   не мешает: SDK 2.2.0 работает, проверено.
2. **Extended thinking.** Параметр бюджета рассуждения у новых моделей Claude устарел, поэтому на
   слайде 18 нет слов про «бюджет» — только про оплату и место в контексте.
3. **Схема слайда 9** взята из лекции 2 как есть. В ней у сервера практики 3 названы `resources`
   и `prompts` — на практике 3 их нет, только `tools`; вслух сказать, что это на лекции 5.
