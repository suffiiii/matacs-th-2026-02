# AI Proposal Triage Design - MATACS Assessment

Candidate Name: Muhammad Sufyan  
Reference: MATACS-TH-2026-02  
Time Spent: 50 minutes  

## Repository Structure & Links
- [Process Flow Diagram](diagram/process_flow.png)
- [Design Write-Up](WRITEUP.md)
- [AI Prompts Specification](PROMPTS.md)
- [Proposal Ranking Results](ranking.json)

## Statement on AI Tool Usage
I utilized Claude 3.5 Sonnet as an analytical partner to generate and validate the structured evaluation schemas. During the iterative process, I challenged the initial automated approach regarding edge cases:
1. I instructed the system to completely withhold **Proposal C** from the competitive ranking (`rank: null`, `status: "flagged"`) due to prompt injection text, rather than assigning it a competitive rank based solely on legitimate text.
2. I enforced a strict disqualification gate on **Proposal B** (`status: "disqualified"`) for lacking a direct ECRA/ESA electrical licence at submission time.