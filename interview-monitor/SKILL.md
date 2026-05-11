---
name: interview-monitor
description: Use when the user provides or references a job description, resume, CV, LinkedIn profile, portfolio, candidate background, interviewer-style interview questions, mock interview prompts, JD-resume fit questions, or numbered answers to interview questions that need scoring, critique, frameworks, ideal logic, professional sample answers, or an HTML answer-analysis report.
---

# Interview Monitor

## Overview

Generate interview questions from an interviewer's perspective by cross-reading the job description and the candidate's resume. When the user answers generated questions, evaluate each answer and create a static, readable HTML report with scoring, expert critique, strategic framework, ideal logic roadmap, and a professional sample answer.

## Mode Selection

- Use **Question Generation Mode** when the user provides a JD and resume/background and wants interview questions.
- Use **Answer Evaluation Mode** when the user provides answers to interview questions, especially numbered answers such as `1. ...`, `2. ...`.
- If evaluating answers, use the original questions from the current conversation when available. If a user provides answers without the matching questions, ask for the questions unless the answer text clearly includes enough context to infer them.

## Question Generation Mode

### Workflow

1. Confirm the input includes both a JD and resume-like candidate background. If one is missing, ask for the missing artifact unless the user explicitly wants questions from only one source.
2. Extract the JD's core hiring signals: role scope, must-have skills, nice-to-have skills, seniority, domain context, responsibilities, collaboration model, and measurable outcomes.
3. Extract resume evidence: relevant roles, projects, achievements, metrics, tools, domains, leadership examples, transitions, and unexplained gaps.
4. Map JD signals to resume evidence:
   - **Strong match**: Resume contains direct evidence for a JD requirement.
   - **Partial match**: Resume has adjacent evidence that needs validation.
   - **Gap or risk**: JD emphasizes something absent or weak in the resume.
5. Build interview threads that cover the JD and resume as fully as practical. Create threads around related themes such as role strategy, product scope, technical architecture, delivery, risk, stakeholder management, and resume-specific projects.
6. Draft enough questions to cover the important signals; do not force or optimize for a fixed ratio of JD-only, resume-only, or JD+resume questions. Still provide at least 10 questions unless the user requests another count.
7. Place related questions together. When one question depends on a prior answer, make it a follow-up in the same thread instead of scattering it elsewhere.

### Question Quality Rules

- Write as an interviewer asking the candidate directly.
- Maximize coverage of both JD and resume. Prefer questions that connect both artifacts, but include JD-only or resume-only questions when needed to cover important requirements, gaps, risks, or distinctive candidate experience.
- Avoid generic prompts such as "請自我介紹" unless adapted to the target role and resume.
- Do not invent candidate facts, company facts, metrics, technologies, or JD requirements.
- If a resume detail is ambiguous, phrase the question as validation: "你的履歷提到 X，可以說明..."
- Surface fit risks constructively: ask about missing requirements, shallow experience, short tenure, career pivots, scale gaps, domain gaps, or seniority gaps when relevant.
- Match question depth to the role. For senior roles, include strategy, tradeoff, leadership, stakeholder, and ambiguity questions. For technical roles, include implementation, architecture, debugging, quality, and operational tradeoff questions.
- Sequence questions as an interviewer would naturally ask them: start with the theme, ask the core question, then add deeper follow-ups about tradeoffs, failure cases, metrics, ownership, or lessons learned.
- Avoid producing isolated one-off questions when they belong to a larger topic. Group them under the same theme or mark them as follow-ups.
- Use the user's language. If the user writes in Traditional Chinese, answer in Traditional Chinese.

### Question Output Format

Start with a brief focus summary:

- Target role focus: 2-4 bullets from the JD.
- Resume-based interview angles: 2-4 bullets from the candidate background.

Then provide grouped interview threads. Each thread should include a concise theme title and a table with at least these columns:

| # | 類型 | 面試問題 | 追問/前後關係 | 為什麼問 / 觀察點 | 依據 |
|---|---|---|---|---|---|

Use concise type labels such as:

- `JD+履歷`
- `履歷深挖`
- `JD缺口`
- `情境題`
- `行為題`
- `技術題`
- `管理/協作`

The `依據` column should name the JD requirement, resume evidence, or gap being tested. Add optional follow-up questions only when they materially improve the interview.

Use `追問/前後關係` to keep dependent questions together. Examples:

- `主問題`
- `追問上一題：風險控管`
- `追問上一題：MVP 取捨`
- `延伸履歷專案：資料流設計`
- `驗證 JD 缺口：智能合約經驗`

## Answer Evaluation Mode

When the user provides answers to interview questions, evaluate every answered question individually.

### Evaluation Workflow

1. Pair each user answer with the matching question. Preserve the user's numbering when possible.
2. For each question, score the answer from 0 to 100 in two dimensions:
   - **Logic Consistency**: Does the answer directly address the question, follow a coherent reasoning chain, avoid contradictions, explain cause/effect, and connect claims to concrete experience or the JD?
   - **Conciseness**: Does the answer stay focused, prioritize the strongest points, avoid unnecessary background, and communicate with high signal density?
3. Calculate an **Overall Score** from 0 to 100 as the rounded average of Logic Consistency and Conciseness unless the user requests another scoring method.
4. Analyze the answer from an **Expert Perspective**:
   - What the answer does well.
   - What is missing, weak, vague, risky, or likely to trigger follow-up pressure from an interviewer.
   - What the candidate should add, remove, or reorder.
5. Provide a **Strategic Framework** for answering that question. Give the framework a memorable name and define the sequence, e.g. `RSM: Risk Boundary -> Strategy Parameters -> Module Architecture`.
6. Provide an **Ideal Logic Roadmap** with the user's score and the key logic steps a strong answer should cover. Break the roadmap into concrete points the candidate should mention.
7. Provide a **Standard Professional Answer** written as a polished candidate response. Make it concrete, logical, and easy for a real candidate to say out loud. Professional means clear reasoning and specific examples, not piling up jargon.

### Scoring Guidance

- Use 90-100 for answers that are structured, specific, complete, concise, and clearly tied to interviewer intent.
- Use 75-89 for strong answers with minor omissions, light verbosity, or slightly underdeveloped examples.
- Use 60-74 for partially strong answers that answer the question but miss important logic, evidence, tradeoffs, or structure.
- Use 40-59 for vague or incomplete answers that show some relevant understanding but would need substantial interviewer probing.
- Use 0-39 for answers that are mostly off-topic, contradictory, unsupported, too shallow, or fail to answer the question.
- Be candid but constructive. Do not inflate scores to be polite.

### Required Per-Question Sections

For each answered question, include these five sections:

1. **Question & User Answer**
   - Show the original question.
   - Show the user's answer verbatim or lightly cleaned for formatting only.
   - Show Logic Consistency, Conciseness, and Overall Score.
2. **Expert Perspective**
   - Explain what is good.
   - Explain what is missing.
   - Explain how an interviewer would likely interpret the answer.
3. **Strategic Framework**
   - Name a suitable framework.
   - Define each step.
   - Explain why the framework fits the question.
4. **Ideal Logic Roadmap**
   - Show the Overall Score prominently as `N/100`.
   - List the ideal answer logic in order.
   - Include the key points that should be mentioned for full credit.
5. **Standard Professional Answer**
   - Write a complete, interview-ready answer using the strategic framework and ideal roadmap.
   - Keep the voice professional, specific, and natural.

### Standard Professional Answer Style

The sample answer should sound like a strong but normal candidate in a real interview.

- Prefer plain language over specialized terminology. Use technical terms only when they are necessary, then immediately explain what they mean in concrete terms.
- Make every important claim observable: describe what the candidate would check, decide, build, limit, measure, or communicate.
- Use cause-and-effect logic: "Because X risk exists, I would do Y, and I would know it works by watching Z."
- Tie abstract ideas back to the candidate's actual experience, JD requirements, product constraints, or interviewer concern.
- Avoid empty professionalism: do not make the answer sound stronger by listing frameworks, architecture terms, or risk-control buzzwords without explaining the action behind them.
- Avoid overly formal phrasing that a person would not naturally say in an interview.
- If a framework has an English name, use it as a quiet organizing aid, but the answer itself should read like a natural explanation rather than a framework lecture.
- Include concrete boundaries when relevant, such as limits, thresholds, sequence of steps, fallback plans, stakeholder checks, or examples of tradeoffs.

When revising a user's answer, convert vague statements into concrete logic. For example:

- Weak: "I would strengthen risk control and monitoring."
- Better: "I would set a maximum number of add-on orders, stop the strategy after a daily loss limit, and pause trading if the exchange API returns inconsistent order status."

- Weak: "I would use a scalable architecture."
- Better: "I would separate order placement, balance checking, and risk checks so a failed API call cannot accidentally trigger duplicate orders."

## HTML Report Requirements

When using Answer Evaluation Mode, output the analysis as a static HTML file, not only as chat text.

- Create a self-contained `.html` file in the current working directory unless the user requests another path.
- Make it readable without a server. Use inline CSS and vanilla JavaScript only.
- Provide question navigation so the user can freely switch between questions. Use tabs, a sidebar, segmented buttons, or another clear static interaction pattern.
- Each question view must contain the five required sections as independent visual blocks.
- Include a summary dashboard at the top with each question's Overall Score, Logic Consistency, Conciseness, and a short issue label.
- Keep typography clean and dense enough for interview prep. Avoid decorative or marketing-style layout.
- Use semantic HTML headings and accessible buttons. The active question should be visually clear.
- Escape user-provided text in HTML so answers render as text, not executable markup.
- In the final chat response, link to the generated HTML file and briefly state how many answers were analyzed.

## Handling Sparse Inputs

If the JD or resume is too short:

- State the limitation briefly.
- Still provide the best possible questions from available evidence.
- Mark weaker assumptions in the `依據` column.
- Ask for the missing artifact or missing detail after the question list, not before, unless the task cannot proceed.
