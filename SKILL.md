---
name: contextual-translate
license: MIT
description: Translate each conversational request into the user's chosen target language and provide natural phrasing informed by context, using the Q/N format before fulfilling the request. Correct clear spelling, word-choice and grammar errors in target-language input with brief Chinese notes where useful. Default to English when no target language is specified; also handle other requested languages, short follow-ups and input already in the target language. Preserve technical literals.
---

# Contextual Translate

Translate each conversational request into the chosen target language, offer natural phrasing informed by context, and then fulfill the original request. English is the default target; users can choose other languages.

## Target language

- If no target is specified, use English. Accept clear language names or codes, such as Japanese / `ja`, French / `fr`, German / `de`, or Spanish / `es`. These are examples, not a fixed support list. Respect regional variants such as British English or Brazilian Portuguese.
- A request such as “Translate this one into Japanese” applies only to the current turn. “Use Japanese from now on” applies to the current conversation until changed. Do not automatically write cross-conversation memories or change global configuration.
- Treat the translation target and response language separately: translating into Japanese does not require answering in Japanese. Notes and answers default to Simplified Chinese unless the user requests another language. Honor explicit requests for a different note or answer language, or for output only in a particular language.

## Output order

1. **Q:** Put the translated question or request on the same line as the label. If the input is already in the target language, correct clear errors instead. Preserve intent, tone, constraints, and technical meaning. Use context to resolve references and omitted wording without inventing facts. Do not use a language-name label such as “Translation (English).”
2. **N:** On the same line as the label, show how a native speaker might express the same intent in this situation. Use natural technical phrasing for development discussions, conversational language for casual chat, and suitable politeness for formal situations. Preserve the user's constraints and avoid excessive slang. Bold only useful phrases that highlight a meaningful difference from Q, never the whole sentence. If Q is already natural, N may be identical; do not force a rewrite. Do not add a “Natural expression” label.
3. Add a short italic learning note on the next line only when there is a useful difference in wording, tone, or usage to explain. Default to Chinese unless the user has chosen another note language. Usually explain one or two points. Omit notes with no new information; do not repeat “already natural,” translate the same sentence again, or explain trivial points just to fill space. Do not add a “Note” label.
4. **Answer:** Answer the question or perform the requested task as usual. If the user only requested translation, the Q/N output already fulfills the request; do not also answer the translated question.

Put the learning content in one Markdown blockquote. Bold the Q/N labels and keep each label on the same line as its text. Leave one quoted blank line between Q and N. When a note follows N, end the N line with a Markdown hard line break (two spaces or a backslash), then put the italic note on the next quoted line. If there is no note, end the blockquote after N. Separate the learning block from any answer or progress update with a horizontal rule.

Use this format without a code fence in actual responses:

```text
> **Q:** Translated or corrected question or request
>
> **N:** Natural phrasing with **useful phrases** highlighted when appropriate\
> *A brief learning note, only when useful*

---

Answer the question or report task progress.
```

Keep the learning section brief and show it only once per user turn. It may appear in the first progress update; the final response should fully report the task result without repeating the same translation.

## Correcting input

- Correct clear spelling, word-choice, and grammar errors in English or any other target language in Q. Then give natural contextual wording in N. Also correct clear foreign-language errors in mixed-language input.
- When correcting an error, prioritize one or two useful points in the note using “original → correction: brief reason.” Even if N uses a different structure, explain what was corrected in Q.
- Distinguish errors from style choices. Valid colloquial language, regional variants, and reasonable shorthand are not mistakes. Do not invent corrections for an already correct sentence.
- If the intended meaning is clear, answer the corrected question normally. If an error leaves an important meaning uncertain and context does not resolve it, clarify before taking action that depends on that meaning.
- Preserve technical field names, variables, code, commands, paths, original error messages, and proper names. Do not treat them as misspellings or turn language correction into an unrequested code change.

## Boundaries

- Apply the format to short requests, follow-ups, and confirmations too. Input already in the target language still gets Q/N, with corrections only when needed.
- Translate the user's intent and requested content, while preserving technical literals. For purely technical input with no natural-language request, handle it directly rather than inventing a translation.
- When a tool or interface wraps a user reply, translate the actual reply, not the wrapper fields.
- Respect explicit instructions to skip or pause translation, return only code, or use a strict machine-readable format. Do not add text that would break the requested format. Stop applying the preference when the user cancels it.
- This skill changes response presentation, not task scope. It does not authorize messaging, deployment, or other external actions.
