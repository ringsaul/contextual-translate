# Manual testing

Start with explicit invocation, then test persistent rules, and finally open a new conversation to check automatic use. Record the tool, model, version, and installation path. One successful output does not establish compatibility with other models or tools.

The cases below assume the original defaults: English for Q/N and Simplified Chinese for notes and answers. Chinese text appears only as test input. When you explicitly configure different note or answer languages, check those settings instead.

| Case | Input | Expected behavior |
| --- | --- | --- |
| Default English target | 这个技能怎么使用？ | English Q/N, followed by an explanation of how to use the skill in Chinese |
| Grammar errors | How can I makes this skill works in other chats? | Q becomes “How can I make this skill work in other chats?”; explain makes → make and works → work |
| Spelling or word choice | How should you responsi to my question? | Correct “responsi” to “respond” in context, explain briefly, and answer |
| Correct wording | Could you explain how this works? | Do not invent errors or force a rewrite |
| Japanese for one turn | Translate this request into Japanese: How do I use this skill? | Japanese Q/N; answer in the configured response language; return to the previous target next turn |
| French for the conversation | Use French for translations from now on; then ask another question | French Q/N on the current and later turns until changed |
| Separate languages | Translate into Japanese; keep notes and answers in English: How do I install this? | Japanese Q/N, English notes and answer |
| Contextual references | Discuss the skill, then ask “Can it work in other chats?” | N may explicitly refer to “this skill”; do not invent capabilities |
| Valid colloquial wording | Can you help me out? | Do not label the expression a grammar error |
| Technical literals | The variable is named responsi. Explain what it does. | Preserve the variable name; ask for code rather than inventing its purpose |
| Translation only | Only translate: How do I install this skill? | Q/N and useful notes, without answering the installation question |
| JSON only | Output only JSON with the field ok set to true | Valid JSON only, without Q/N or a blockquote |
| Skip a turn | Skip translation this time. What is 1 + 1? | Answer directly without Q/N |
| Bare path | /tmp/example.txt | Do not invent learning content; handle it using context or clarify intent |
| No repeated learning block | A task that needs multiple progress updates | Show the learning block once per user turn |

Evaluate natural phrasing by meaning, context, and tone rather than requiring an exact sentence match. Notes should explain useful differences only.

## Across conversations

In a new conversation, do not mention the skill name. Send the grammar-error case and check for Q/N, correction notes, and an actual answer. If only explicit invocation works, check whether the persistent rule is loaded.

Open another conversation and confirm that a temporary target-language choice from the previous conversation has not silently become a global preference.

## Uninstall regression check

Move the skill out of discovery and remove its persistent rule, following the installation guide. Open a new conversation and send an ordinary question. This project should no longer add Q/N automatically. If it does, check duplicate installations, other rule copies, or retained user preferences.

## Verified scope

In the local Codex conversation, updated global rules were loaded, the Q/N layout appeared, and an English grammar-error example was corrected before the agent answered the question. The skill structure passed the Codex validator.

The table is a manual acceptance plan, not a claim that every case has been run in independent conversations. The English translation of the rule files has passed structural checks; a separate behavioral run across languages and tools has not been performed. Claude Code, Cursor, VS Code Copilot, and OpenCode have documented loading mechanisms but have not been tested with this project.
