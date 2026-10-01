---
marp: true
theme: default
size: 16:9
paginate: true
lang: ru
title: "Занятие 3. Инструмент, рассуждение, память, контекст. MCP руками"
description: "РУТ (МИИТ), 09.04.01. Генеративный ИИ и ИИ-агенты для транспортной логистики"
style: |
  /* ── Палитра и типографика ─────────────────────────────────────────── */
  :root {
    --ink:    #14161a;   /* основной текст */
    --muted:  #6b7280;   /* второстепенное */
    --accent: #1d4ed8;   /* акцент: цифры и ключевые термины */
    --rule:   #e5e7eb;   /* линейки */
    --tint:   #f4f6fb;   /* подложка слайдов «двух форм» */
  }
  section {
    font-family: "PT Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 27px;
    line-height: 1.45;
    color: var(--ink);
    background: #fff;
    padding: 52px 64px 64px;
    /* Тема по умолчанию центрирует содержимое по вертикали, из-за чего
       верхняя треть слайда пустует. Центрует именно align-content: safe center
       (в современном CSS оно работает и для блочных контейнеров), а не
       justify-content — его переопределение ни на что не влияет.
       Контентные слайды прижимаем кверху. */
    align-content: start;
  }
  h1, h2 { letter-spacing: -0.01em; }
  h1 { font-size: 46px; margin: 0 0 14px; }
  h2 {
    font-size: 34px; margin: 0 0 18px; padding-bottom: 10px;
    border-bottom: 3px solid var(--rule);
  }
  h3 { font-size: 25px; color: var(--muted); margin: 0 0 12px; font-weight: 600; }
  p  { margin: 0 0 14px; }
  ul, ol { margin: 0 0 14px; padding-left: 26px; }
  li { margin-bottom: 7px; }
  /* Цифры и ключевые термины — главное на слайде, их и выделяем цветом */
  strong { color: var(--accent); font-weight: 700; }
  code { background: #f3f4f6; padding: 1px 6px; border-radius: 4px; font-size: 0.9em; }
  a { color: var(--accent); }

  /* ── Таблицы ────────────────────────────────────────────────────────── */
  table { font-size: 22px; border-collapse: collapse; width: 100%; }
  th {
    text-align: left; font-size: 19px; text-transform: uppercase;
    letter-spacing: 0.06em; color: var(--muted); font-weight: 700;
    border-bottom: 2px solid var(--ink); padding: 8px 12px;
  }
  td { padding: 8px 12px; border-bottom: 1px solid var(--rule); vertical-align: top; }
  tr:last-child td { border-bottom: none; }
  table strong { color: var(--ink); }

  /* ── Титул ──────────────────────────────────────────────────────────── */
  section.lead { align-content: safe center; }
  section.lead h1 { font-size: 54px; line-height: 1.15; }
  section.lead h3 { color: var(--accent); font-weight: 700;
    text-transform: uppercase; letter-spacing: 0.08em; font-size: 21px; }

  /* ── Представление лектора ─────────────────────────────────────────── */
  section.profile-slide { align-content: safe center; }
  .profile {
    display: flex; align-items: center; gap: 52px; width: 100%;
  }
  section.profile-slide .profile-photo {
    flex: 0 0 300px; width: 300px; height: 450px; max-height: none;
    margin: 0; object-fit: cover;
  }
  .profile-name {
    margin: 0 0 18px; color: var(--accent); font-size: 52px;
    font-weight: 700; line-height: 1.1; letter-spacing: -0.02em;
  }
  .profile-role { margin: 0; font-size: 32px; line-height: 1.25; }

  /* ── Разделители блоков ─────────────────────────────────────────────── */
  section.divider {
    align-content: safe center;
    background: var(--ink); color: #fff; justify-content: center;
    padding-left: 72px;
  }
  section.divider h1 { color: #fff; font-size: 58px; margin-bottom: 8px; }
  section.divider h3 { color: #9aa4b2; font-size: 27px; font-weight: 400; }
  section.divider strong { color: #fff; }
  section.divider::after { color: #4b5563; }

  /* ── Вопрос аудитории ───────────────────────────────────────────────── */
  section.question {
    align-content: safe center;
    background: var(--tint); justify-content: center;
    border-left: 20px solid var(--accent);
  }
  section.question h1 { font-size: 42px; color: var(--accent); }

  /* ── Возврат к двум формам: сквозная линия лекции ───────────────────── */
  /* Эти слайды повторяются пять раз и должны узнаваться мгновенно. */
  section.forms {
    align-content: safe center;
    background: var(--tint); border-left: 20px solid var(--ink);
  }
  section.forms h2 {
    font-size: 30px; border-bottom: none; color: var(--muted);
    text-transform: uppercase; letter-spacing: 0.06em; font-size: 21px;
  }
  section.forms p { font-size: 29px; }

  /* ── Ключевые слайды сквозного тезиса (открытие и закрытие) ────────── */
  section.thesis {
    align-content: safe center;
    background: var(--tint); border-left: 20px solid var(--accent);
  }
  section.thesis h2 { font-size: 36px; border-bottom: 3px solid var(--accent); }
  section.thesis p { font-size: 28px; }

  /* ── Крупные цифры ──────────────────────────────────────────────────── */
  .huge { font-size: 92px; font-weight: 800; line-height: 1.0; color: var(--accent); letter-spacing: -0.03em; }
  .big  { font-size: 66px; font-weight: 800; line-height: 1.05; color: var(--accent); letter-spacing: -0.02em; }
  .mid  { font-size: 40px; font-weight: 700; line-height: 1.15; color: var(--accent); }
  .muted { color: var(--muted); font-size: 20px; }

  /* ── Схемы ──────────────────────────────────────────────────────────── */
  section img { display: block; margin: 6px auto 0; max-height: 480px; }

  /* ── Код: определения инструментов и ответы API ─────────────────────── */
  /* Лекции 1 эти правила не нужны: там не было ни одного блока кода.
     Здесь кодом показывается механика вызова, и без явного размера
     тема по умолчанию даёт слишком мелкий моноширинный шрифт. */
  pre {
    background: #f6f7f9; border-left: 6px solid var(--rule); border-radius: 6px;
    padding: 14px 20px; margin: 0 0 14px; overflow: hidden;
  }
  pre code { font-size: 19px; line-height: 1.4; background: none; padding: 0; }
  section.code-tight pre code { font-size: 16px; line-height: 1.35; }

  /* ── Слайд-акцент: одна фраза во весь экран ─────────────────────────── */
  section.punch {
    align-content: safe center;
    justify-content: center; background: var(--ink); color: #fff;
  }
  section.punch h1 { color: #fff; font-size: 50px; line-height: 1.2; }
  section.punch p { color: #cbd5e1; font-size: 26px; }
  section.punch strong { color: #93b4ff; }
  section.punch::after { color: #4b5563; }

  /* ── Колонтитул и нумерация ─────────────────────────────────────────── */
  section::after {
    font-size: 17px; color: var(--muted);
    right: 40px; bottom: 26px;
  }
---

<!-- _class: lead -->

# MCP, рассуждение, память, контекст.  

### Занятие 3 из 8 · 1 октября 2026

**Генеративный искусственный интеллект и ИИ-агенты для транспортной логистики**
РУТ (МИИТ) · 09.04.01 Информатика и вычислительная техника

---

## План вечера

| Часть | Минуты | Что |
|---|---|---|
| 1. Вводная лекция | 30 | четыре элемента одного цикла: инструмент (свой и MCP), рассуждение, память, контекстное окно |
| 2. Практика | 60–90 | три инструмента из практики 2 переезжают на MCP-сервер; рассуждение и контекст — в логе цикла |
| 3. Итоги | 30 | кейсы из жизни и разговор о ваших проектах |

Сегодня занятие одним блоком, **2–2,5 часа**.

---

## Ваш проект  

**Рамок нет.** От агента, который генерирует рекламные шортсы, до ИИ-агента ССП. Логистика и учебные данные — не обязательны. Идеи у команд могут совпадать.

Требование одно: **это агент** — модель сама выбирает инструменты в цикле.

Команда **2–3 человека**. 

---

## Идеи для проекта

| Идея                        | Инструменты                                        | 
|-----------------------------|----------------------------------------------------|
| **Анализ тендеров**         | поиск и загрузка документации, извлечение требований | 
| **Ассистент задач команды** | приём задач, трекер, напоминания                   | 
| **Агент-блогер**            | сбор текстов конкурентов, публикация               | 
| **Агент-исследователь**     | поиск конкурентов по теме, сбор их стилей          | 
| **Агент-контент**           | планирвоание и создание цикла рилсов по теме | 




---

<!-- _class: thesis -->

## Идея лекции и практики

Цикл из практики 2 — это четыре логических блока:
- Модель **рассуждает**, что позвать;
- **Инструмент** считает;
- Всё, что вернулось, ложится в **контекст**;
- То, что должно пережить разговор, уходит в **память**.

Сегодня рассмотрим каждый блок подробнее.

---

<!-- _class: divider -->

# Часть 1. Вводная лекция

### Четыре элемента одного цикла — по одному блоку на каждый

---

## Карта лекции

![w:980](assets/lecture-map.svg)

<span class="muted">Схема курса по циклу практики 2; стрелки — те же, что на схеме вызова из лекции 2.</span>

---

<!-- _class: divider -->

# Блок 1 из 4 · Инструмент

### Свой — или MCP. Что меняется, когда инструмент уезжает из вашего процесса

---

## Зачем MCP

Инструменты, которые вы написали на прошлом занятии, **живут внутри ноутбука**. Другое приложение их не позовёт.

**MCP** — открытый стандарт подключения ИИ-приложений к внешним системам. Способ вынести инструменты в **отдельный процесс**, чтобы позвать мог кто угодно.


<span class="muted">modelcontextprotocol.io, «What is MCP»: «MCP (Model Context Protocol) is an open-source standard for connecting AI applications to external systems».</span>

---

## Свой инструмент и MCP-инструмент: три разреза

|                                   | Свой (практика 2) | MCP (практика 3) |
|-----------------------------------|---|---|
| **Где работает код**              | обычная функция внутри ноутбука; вызываем её по имени | отдельная программа (сервер); клиент отправляет ей запрос `tools/call` |
| **Откуда приложение знает, какие инструменты есть** | вы сами выписали список `TOOLS` | спрашивает у сервера запросом `tools/list` при запуске — заранее имён в коде клиента нет |
| **Кто пишет то, что видит модель** | вы: описание инструмента, текст ошибки, длину ответа | автор сервера, не вы. Вы пишете только клиент; ошибка приходит с флагом `isError`, а её текст и размер ответа задаёт сервер |

Модель в обоих случаях видит **ровно одно и то же**: имя, описание, схему.

<span class="muted">Первые два разреза — таблица лекции 2 и MCP «Architecture overview». Третий — вывод курса, к нему вернёмся в блоке 4.</span>

---


<!-- _class: divider -->

# Блок 2 из 4 · Рассуждение

### Этапы работы LLM до ответа пользователю

---

## Chain-of-thought: шаги до ответа

Модель, которая пишет **промежуточные шаги** до ответа, решает многошаговые задачи лучше: арифметику, задачи на здравый смысл, символьные.

Хватает даже одной фразы: **«давайте подумаем шаг за шагом»**.


<span class="muted">Wei et al., Google, 2022: «chain of thought prompting improves performance on a range of arithmetic, commonsense, and symbolic reasoning tasks». Kojima et al., 2022: «LLMs are decent zero-shot reasoners by simply adding "Let's think step by step" before each answer».</span>

---

## Рассуждение в цикле агента

На лекции 2 был **ReAct**: мысль → действие → наблюдение → снова мысль.

«Мысль» между вызовами инструментов — **тот же chain-of-thought**, только теперь после него идёт не ответ, а вызов.

В вашем цикле из практики 2 рассуждение решает одно: **какой инструмент позвать и с какими аргументами**.

<span class="muted">Yao et al., ReAct, 2022: «generate both reasoning traces and task-specific actions in an interleaved manner».</span>

---

## Куда развивается рассуждение

![w:960](assets/reasoning-lineage.svg)

<span class="muted">Yao et al., ToT, 2023: «considering multiple different reasoning paths and self-evaluating choices». Wang et al., Plan-and-Solve, 2023: «devising a plan to divide the entire task into smaller subtasks».</span>

---

## Ветвление: Tree of Thoughts

![w:600](assets/tot-fig1.png)

Chain-of-thought (c) идёт по **одной** цепочке. ToT (d) **предлагает несколько мыслей, оценивает, выбирает лучшие** и при тупике **откатывается**. Зелёное — выбрано, розовое — отброшено.

«Игра 24»: GPT-4 с chain-of-thought — **4 %**, с ToT — **74 %**.

<span class="muted">Yao et al., ToT, 2023, рис. 1: «considering multiple different reasoning paths and self-evaluating choices to decide the next course of action, as well as looking ahead or backtracking when necessary». Цифры — из аннотации статьи. В цикле агента это значит: перед вызовом инструмента модель сравнивает варианты, а не берёт первый.</span>

---

## План до действий: Plan-and-Solve

![w:520](assets/plan-and-solve-fig2.png)

Одна задача, одна модель, разная фраза. (a) «Подумаем шаг за шагом» → **55 %**, неверно. (b) «Сначала составим план, потом выполним» → **60 %**, верно.

<span class="muted">Wang et al., Plan-and-Solve, 2023, рис. 2: «first, devising a plan to divide the entire task into smaller subtasks, and then carrying out the subtasks according to the plan». Целится в ошибку «пропущен шаг». В цикле агента — строка плана в первой мысли.</span>

---

## Self-reflection — и её граница

**Reflexion:** агент разбирает обратную связь по своей попытке, записывает вывод в память и учитывает его в следующей попытке.

**Граница:** без **внешней** обратной связи модель исправляет себя плохо, а иногда ответ после «самопроверки» становится хуже.

Внешняя обратная связь для агента — **результат инструмента**. В том числе текст ошибки, который вы возвращали в TODO 2 практики 2.

<span class="muted">Shinn et al., Reflexion, 2023: «verbally reflect on task feedback signals, then maintain their own reflective text in an episodic memory buffer». Huang et al., Google DeepMind, 2023: «LLMs struggle to self-correct their responses without external feedback, and at times, their performance even degrades after self-correction».</span>

---

## Reflexion на примере

![w:900](assets/reflexion-fig1.png)

Три задачи, одна схема. (b) попытка не удалась → (c) оценка: подсказка среды, упавший тест или «0» → (d) **модель словами записывает, что пошло не так** → (e) следующая попытка с этой записью перед глазами. Красное — ошибка, зелёное — исправление.

<span class="muted">Shinn et al., Reflexion, 2023, рис. 1: «verbally reflect on task feedback signals, then maintain their own reflective text in an episodic memory buffer».</span>

---

## Reasoning-модели: рассуждение за деньги

Рассуждение встроено в модель. Пользователю оно целиком не показывается, но **оплачивается как выходные токены** и **занимает место в контексте**.

Правило курса: платить за рассуждение, когда задача **многошаговая**. На «сколько выгрузили в марте» оно не нужно — там нужен инструмент.

<span class="muted">Claude Docs, «Thinking: steering and cost»: «Tokens Claude uses while thinking (billed as output tokens)». OpenAI, «Reasoning models»: «they still occupy space in the model's context window and are billed as output tokens». Правило — вывод курса.</span>

---

<!-- _class: punch -->

# Рассуждение помогает выбрать инструмент. **Число считает инструмент.**

Рассуждение повышает шансы на верный ход, но точного числа не гарантирует.

---

<!-- _class: divider -->

# Блок 3 из 4 · Память

### Кратковременная, долговременная — и почему это ещё один инструмент

---

## Память — третье расширение модели

Агентные системы строятся на основе LLM-модель, к которой подключены три расширения. Это поиск по внешним данным, инструменты и память». 

<span class="muted">Anthropic, «Building effective agents»: «The basic building block of agentic systems is an LLM enhanced with augmentations such as retrieval, tools, and memory».</span>

---

## Два вида памяти

![w:960](assets/memory-types.svg)

<span class="muted">Sumers, Yao, Narasimhan, Griffiths. CoALA, 2023: «Working memory maintains active and readily available information… for the current decision cycle» · «Episodic memory stores experience from earlier decision cycles» · «Semantic memory stores an agent's knowledge about the world and itself».</span>

---

## Долговременная память — это инструмент

У Anthropic долговременная память оформлена **буквально как инструмент**: модель просит операцию с файлом, а выполняет и хранит данные **ваше приложение**.



<span class="muted">Claude Docs, «Memory tool»: «The memory tool operates client-side: Claude requests file operations, and your application executes them». Park et al., Stanford, 2023: «store a complete record of the agent's experiences… synthesize those memories over time into higher-level reflections, and retrieve them dynamically».</span>

---

<!-- _class: divider -->

# Блок 4 из 4 · Контекстное окно

### Ограниченный ресурс, за который платят на каждом вызове

---

## Вся память вашего агента прямо сейчас

![w:980](assets/messages-growth.svg)

<span class="muted">Прогон эталона практики 2: 2 итерации, 1 вызов инструмента; 9 761 — notebooks/data/agent_facts.json.</span>

---

## Длинный контекст читается хуже

Контекст — **ограниченный ресурс с убывающей отдачей**: чем длиннее вход, тем хуже модель им пользуется, и деградирует она неравномерно.

Каждый результат инструмента **остаётся в списке** до конца цикла — и уходит в модель заново на каждом вызове.

Отсюда правило лекции 2: инструмент возвращает **ответ, а не все данные**. 

<span class="muted">Anthropic, «Effective context engineering for AI agents», 2025: «context… must be treated as a finite resource with diminishing marginal returns». Chroma, «Context Rot», 2025: «model performance degrades as input length increases, often in surprising and non-uniform ways».</span>

---

## Середину контекста модель теряет

![h:400](assets/lost-in-the-middle-fig1.png)

Нужный документ находится в начале или в конце контекстного окна— точность выше. **В середине — ниже**, чем без документов вовсе (пунктир).

<span class="muted">Liu et al., Stanford, 2023, рис. 1: «performance is often highest when relevant information occurs at the beginning or end of the input context, and significantly degrades… in the middle of long contexts».</span>

---

## Три приёма против роста контекста

| Приём | Что делает |
|---|---|
| **Сжатие (compaction)** | разговор у предела окна сворачивается в сводку, работа продолжается с ней |
| **Заметки вне контекста** | агент сам записывает важное в память вне окна и читает по запросу |
| **Очистка результатов инструментов** | старые результаты убираются из списка — самая безопасная форма сжатия |


Кэширование промпта снижает **цену и задержку**, но размер контекста не меняет.

<span class="muted">Anthropic, «Effective context engineering»: «summarizing its contents, and reinitiating a new context window with the summary» · «notes persisted to memory outside of the context window» · «one of the safest lightest touch forms of compaction». Packer et al., MemGPT, 2023. Claude Docs, «Prompt caching». Вывод про размер — курса.</span>

---

## Чужой сервер — чужой объём

Результат MCP-инструмента попадает в `messages` **как есть**. Сколько в нём токенов — решил владелец сервера, а не вы.

Правило «ответ, а не таблица» вы больше **не контролируете**. Контролируете клиент: обрезать длинный результат, чистить старые обращения к инструментам.

Это третий разрез таблицы из блока 1: **описание чужое, ошибка по контракту, объём чужой.** Клиент — последний рубеж перед контекстом.

<span class="muted">Anthropic, «Effective context engineering»: очистка результатов инструментов — «one of the safest lightest touch forms of compaction». Вывод про клиент как рубеж — курса.</span>


---

<!-- _class: divider -->

# Часть 2. Практика

### Три инструмента уезжают на MCP-сервер. Цикл этого не замечает

---

## Задание

**Артефакт:** ноутбук `03_mcp_server_client.ipynb` — четыре задания, по одному на элемент агента.

**Сервер** пишется ячейкой `%%writefile server.py` и запускается как **отдельный процесс** (транспорт stdio). Функции над данными — те же, что в практике 2, готовые.

**Цикл агента** — тот же, что вы писали в практике 2; добавлены только ручки для сравнений.

**Критерий:** минимум — `check()` **4/4** (TODO 1–2), полная траектория — **8/8**.

---

## Четыре TODO

| TODO | Что пишете |  
|---|---|
| **1** | `server.py`: `query_load` и `find_wagons` под `@mcp.tool()` по образцу `query_unload`; docstring = описание, аннотации = схема | 
| **2** | `memory_tools.py`: `remember(note)` и `recall()` на том же сервере, файл на его стороне | 
| **3** | `pick_reasoning(question)`: `"none"` или `"low"` — когда модели думать | 
| **4** | `prune_tool_results(messages, keep_last=1)`: старые результаты инструментов → короткая строка | 

---

<!-- _class: divider -->

# Часть 3. Итоги

### Ваши проекты

---

## Ваш проект: тема свободная

**Рамок нет.** От агента, который генерирует рекламные шортсы, до ИИ-агента ССП. Логистика и учебные данные — не обязательны. Идеи у команд могут совпадать.

Требование одно: **это агент** — модель сама выбирает инструменты в цикле.

Команда **2–3 человека**. Заявка — это сегодняшний разговор плюс одно сообщение в issue курса.

---

## Идеи для проекта

| Идея                        | Инструменты                                        |  Память                                        | Контекст                                            |
|-----------------------------|----------------------------------------------------|----------------------------------------------------|-------------------------------|
| **Анализ тендеров**         | поиск и загрузка документации, извлечение требований | | |  
| **Ассистент задач команды** | приём задач, трекер, напоминания                   | | | 
| **Агент-блогер**            | сбор текстов конкурентов, публикация               | | | 
| **Агент-исследователь**     | поиск конкурентов по теме, сбор их стилей          | | | 
| **Агент-контент**           | планирвоание и создание цикла рилсов по теме | | | 




---

## Идеи для проекта

| Идея | Инструменты | Память                                        | Контекст                                            |
|---|---|-----------------------------------------------|-----------------------------------------------------|
| **Анализ тендеров** | поиск и загрузка документации, извлечение требований | что уже просмотрено и отклонено               | документация длинная — разбор по частям             |
| **Ассистент задач команды** | приём задач, трекер, напоминания | кто за что отвечает, сроки                    | история растёт — сводка вместо переписки            |
| **Агент-блогер** | сбор текстов конкурентов, публикация | стиль и прошлые посты                         | тексты конкурентов — выжимка, а не копия            |
| **Агент-исследователь** | поиск конкурентов по теме, сбор их стилей | карта конкурентов, пополняется между сессиями | карта во внешнем хранилище, в контекст — по запросу |
| **Агент-контент**           | планирвоание и создание цикла рилсов по теме | стиль публикации, план проекта       | растет история запросов                             |


---

## Домашнее задание

1. Довести `check()` до **8/8** — на минимальной траектории это TODO 3 и 4 дома.
2. **Механика MCP своими руками:** `my_build_tools` (`tools/list` → формат провайдера) и `my_call_tool` (`tools/call`, `is_error` → текст для модели).
3. **`ToolError` на сервере:** неизвестная станция отдаёт модели причину, а не безликое «Error executing tool».
4. **Четвёртый инструмент `gu12`** — на сервер.
5. **Одно сообщение в issue курса:** состав команды и идея проекта в одну-две фразы.

`check_homework()` проверяет пункты 2 и 3. Следующее занятие — **15 октября**.

<span class="muted">MCP Specification 2026-07-28, Tools: «Tool Execution Errors contain actionable feedback that language models can use to self-correct», «reported in tool results with isError: true».</span>

---

## Что почитать к занятию 4

1. [Anthropic. Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — главное чтение, 20 минут.
2. [Lilian Weng. LLM Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/) — разделы Planning и Memory.
3. К практике: [What is MCP](https://modelcontextprotocol.io/docs/getting-started/intro) и [спецификация MCP, Server / Tools](https://modelcontextprotocol.io/specification/2026-07-28/server/tools).
4. По интересу: [Chain-of-Thought](https://arxiv.org/abs/2201.11903) · [Reflexion](https://arxiv.org/abs/2303.11366) · [Tree of Thoughts](https://arxiv.org/abs/2305.10601) · [Plan-and-Solve](https://arxiv.org/abs/2305.04091) · [Cannot Self-Correct Yet](https://arxiv.org/abs/2310.01798) · [CoALA](https://arxiv.org/abs/2309.02427) · [MemGPT](https://arxiv.org/abs/2310.08560) · [Lost in the Middle](https://arxiv.org/abs/2307.03172).
5. Для проектов с памятью: [Claude Docs, Memory tool](https://platform.claude.com/docs/en/agents-and-tools/tool-use/memory-tool).

<span class="muted">Все ссылки — в slides/lecture-03/SOURCES.md.</span>
