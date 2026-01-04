# AI-Red-Teaming-Llama3.1
Hands-on red teaming of Meta’s Llama 3.1 70B: Exploring jailbreaks, vulnerabilities, and AI safety best practices (2026 case study)

In 2026, generative AI is everywhere. From chatbots to enterprise agents, but so are the risks. Recently, I ran a personal red teaming exercise on Meta’s Llama 3.1 70B Instruct (one of the leading open-source LLMs) to probe for vulnerabilities like jailbreaks, prompt injections, and harmful output generation.
Red teaming involves simulating adversarial attacks to expose weaknesses before malicious actors do. Leading labs like Meta, OpenAI, and Anthropic use it extensively, and I wanted to share a practical, hands-on case study. All testing was done responsibly on a publicly available open-weight model with no sensitive data or production systems involved.
I focused on key risk categories from frameworks like OWASP Top 10 for LLMs and NIST AI RMF:

•  Jailbreaks & Prompt Injections — Bypassing safety guardrails.
•  Harmful Content Generation — Toxicity, bias, misinformation or disallowed topic like Violence.
•  Multi-turn Persistence: Escalating in longer conversations.
•  Other Vectors — Encoded inputs (e.g., Base64), role-playing, and indirect injections.
The tools I used? Manual prompt iteration, simple Python scripts for automation, and evaluation rubrics. I drew inspiration from open-source frameworks like Garak and DeepTeam.

I ran over 150 adversarial scenario. Overall, Llama 3.1 70B showed strong baseline safety, but several medium/high-risk vulnerabilities emerged:
1.  Successful Jailbreak (Medium Risk): Using a role-playing prompt combined with gradual escalation, the model generated detailed instructions for a restricted activity (e.g., hypothetical illegal substance synthesis) after initially refusing.
2.  Prompt Injection & Persistence: In multi-turn chats, the model sometimes “forgot” earlier refusals, especially with encoded or translated inputs.
3.  Harmful Content Gaps: The model robustly refused direct hate speech or violence but was more permissive with cleverly worded or hypothetical requests (e.g., “write a fictional story about…”).
4.  Positive Results: Llama 3.1 70B performed well on toxicity detection and direct harmful requests, often refusing outright or adding disclaimers.
Out of 150 tested scenarios, 18% succeeded in eliciting undesired outputs (medium/high severity). It was a fun experience and I learned a few things: 
•  For Developers: Layered defenses are essential. System prompts alone aren’t enough. Add output filters, rate limiting, and continuous red teaming.
•  Best Practices: Use diverse testers and automate with tools like DeepTeam or PyRIT. Test iteratively during fine-tuning.
•  Broader Implications: Open-weight models like Llama are incredibly powerful, but responsible use requires proactive safety work. This exercise reinforced why red teaming is non-negotiable for trustworthy AI.

Responsible disclosure: No proprietary models tested.

![WhatsApp Image 2026-01-04 at 10 08 18_0a935e63](https://github.com/user-attachments/assets/27370da2-150a-4051-a5fa-47f80d713d59)
![WhatsApp Image 2026-01-04 at 10 08 18_85db375f](https://github.com/user-attachments/assets/8036a680-a70f-4e9a-a9a8-843ede2613ce)
