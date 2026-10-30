# Contextual Translate

[English](README.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md)

**Talk to your agent as usual, and learn how to say the same thing naturally in another language.**

## Why use it?

- **Learn during everyday conversations**: Ask about code or troubleshoot a problem, and see how to express the same request in another language. The agent then continues with your task.
- **Compare Q and N**: Q conveys your meaning in the target language; N shows how a native speaker might phrase it in the same situation.
- **Translate with context**: Use earlier messages to understand references such as “this” and “it,” and keep terminology consistent.
- **Correct spelling and grammar**: Try asking in the language you are learning. Clear errors are corrected, with a short explanation of one or two useful points.
- **Choose translation and response languages separately**: Practice Spanish or French while keeping explanations and answers in English.
- **Keep learning notes short**: Useful phrases appear in bold, with a brief note when needed. Q/N stays separate from the actual answer.

## 1. Ask your agent to install it

Send this message to your agent:

```text
Install this skill for me. Translate my requests into Spanish, and keep learning notes and answers in English: https://github.com/ringsaul/contextual-translate
```

Replace “Spanish” with the language you want to learn. After installation, ask questions as usual. You can change the target language during a conversation.

The agent should follow the [installation guide](docs/installation.md) and `examples/`, add the selected languages and per-turn requirement to the effective rules for this skill, preserve unrelated settings, and report the scope and any reload needed.

See the [installation guide](docs/installation.md) for manual installation, updates, pausing, and removal. The guides, rule examples, and skill instructions are written in English. The request above also sets English for learning notes and answers.

## 2. Full conversation examples

### Translating a question with context

Target language: Spanish. Notes and answers: English.

**User:**

```text
Can this skill use context when translating my questions?
```

**Agent:**

> **Q:** ¿Puede este skill usar el contexto para traducir mis preguntas?
>
> **N:** ¿Puede **tener en cuenta nuestra conversación** al traducir mis preguntas?  
> *“Tener en cuenta” means “take into account.” Here it refers to using the earlier conversation.*

---

Yes. The rules already require the agent to use context when interpreting your request. Earlier messages help resolve references such as “this skill,” understand omitted details, and keep terminology consistent.

Q expresses your meaning; N offers a natural way to say it in context. If the conversation still leaves an important detail unclear, the agent should ask instead of inventing requirements.

### Correcting a grammar mistake

The target language is still Spanish. Here, the user tries asking directly in Spanish.

**User:**

```text
¿Con qué frecuencia debo regar mis planta?
```

**Agent:**

> **Q:** ¿Con qué frecuencia debo regar mis **plantas**?
>
> **N:** ¿Cada cuánto **tengo que regar** mis plantas?  
> *“Mis planta” → “mis plantas”: use the plural noun after “mis” (my, plural). “Cada cuánto” is a common way to ask “how often,” and “tengo que regar” means “I need to water.”*

---

It depends on the plant and how moist the soil is. Check the soil before watering instead of watering every day on a fixed schedule.

What kind of plant is it, and do you keep it indoors or outdoors? That will help me give more specific advice.

The agent corrects the sentence and then answers the question as usual.

## 3. What do Q and N mean?

| Part | Meaning | What you see |
| --- | --- | --- |
| **Q — Question** | Your question or request in the target language | Your intended meaning, with clear spelling, word-choice, or grammar errors corrected if you already used that language |
| **N — Native phrasing** | How a native speaker might say it in this situation | A natural expression informed by context, with useful phrases in bold |
| Italic note below N | A short learning note | One or two useful points about wording or corrections; omitted when there is nothing useful to explain |
| Text after the separator | The agent’s actual response | An answer or task execution, rather than stopping at the translation |

Q does not simply repeat your input, and N is not the answer to your question. Both express your intent; the answer comes afterward. If Q is already natural, N may be identical. There is no need to force a rewrite.

## 4. Corrections and exceptions

- Clear spelling, word-choice, or grammar errors in the target language: correct them in Q and explain one or two key points.
- Valid conversational language or regional variants: do not label them as errors or rewrite them just to make N different.
- An error that makes the meaning unclear: clarify before answering or taking action that depends on that meaning.
- Code, variable names, commands, paths, original error messages, and proper names: preserve them as written.
- Translation-only requests: provide Q/N and useful notes without answering the translated question.
- Requests such as “JSON only,” “code only,” or an explicit instruction to skip translation: omit Q/N when it would break the requested format.

## 5. Choose a translation language

**The target language, learning-note language, and answer language can be set separately.**

This page uses Spanish as the learning language for English-speaking readers. In the [2025 Duolingo Language Report](https://blog.duolingo.com/2025-duolingo-language-report/), Spanish was the most studied language on the platform in the U.S., the U.K., Ireland, Australia, and New Zealand. This is country-level platform data, not a ranking of all native English speakers worldwide. You can choose a different language at any time.

| Tell your agent | Effect |
| --- | --- |
| Translate my requests into Spanish from now on | Use Spanish for this conversation until changed |
| Translate this request into Japanese | Use Japanese for this turn, then return to the previous setting |
| Use French for translations for the rest of this conversation | Keep French as the target for this conversation |
| Translate into German; keep notes and answers in English | Use German for Q/N and English for notes and answers |
| Switch the translation language to Korean | Use Korean for subsequent turns in this conversation |
| Use British English for translations | Use British English wording in this conversation |
| Skip translation this time | Answer directly for this turn |

You can specify a language name, a clear language code, or a regional variant: Spanish / `es`, French / `fr`, Japanese / `ja`, German / `de`, Korean / `ko`, or Brazilian Portuguese, for example. These are examples, not a fixed support list. Language quality depends on the model.

**Want French in every new conversation?** Ask your agent:

```text
Set the global translation language for contextual-translate to French.
Keep learning notes and answers in English.
Save this preference in the effective personal rules block for this skill,
preserve unrelated settings, and explain where the change applies.
```

“This time” and “from now on” affect the current turn or conversation; they do not automatically change other chats. Persistent preferences require an explicit update to the effective personal rules. A tool that only supports project rules will apply the setting within that project.

## 6. Compatible tools

| Tool | Skill loading and persistent rules | Verification |
| --- | --- | --- |
| Codex | `.agents/skills/` and effective `AGENTS.md` rules | Format, corrections, and rule loading observed in the current local Codex conversation |
| Claude Code | `.claude/skills/` and `CLAUDE.md` | Official documentation checked; not tested in this project |
| Cursor | `.agents/skills/`, `.cursor/skills/`, and tool rules | Official documentation checked; not tested in this project |
| VS Code Copilot Agent | `.agents/skills/`, `.github/skills/`, and tool rules | Official documentation checked; not tested in this project |
| OpenCode | `.agents/skills/`, `.opencode/skills/`, and `AGENTS.md` | Official documentation checked; not tested in this project |

See the [compatibility guide](docs/compatibility.md) for directories, personal versus project scope, and official sources. Support for loading `SKILL.md` does not mean this project has been tested in every tool.

## Further reading

Detailed guides and skill instructions:

- [Installation, per-turn setup, updates, pausing, and removal](docs/installation.md)
- [Compatibility and official sources](docs/compatibility.md)
- [Manual test cases](docs/testing.md)
- [Full skill instructions](SKILL.md)

This skill works through instructions. It has no separate translation service and requires no additional API key for the project. The account, subscription, and network requirements of your agent or model still apply. The skill includes no data-upload scripts; requests are handled by the agent and model you use.

The per-turn behavior is an instruction, not an enforced execution hook. Cloud and remote environments need their own installation or synchronization. Language preferences and correction quality depend on the tool, model, and rules actually loaded.

When reporting an issue, include the tool version, model, installation location, and a non-sensitive example of the input and actual output.

---

Author: ringsaul · [MIT License](LICENSE)
