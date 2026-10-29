# MATACS Associate Software Developer Assessment

## Candidate Information
- **Name:** Muhammad Irfan
- **Reference:** MATACS-TH-2026-02
- **Time Spent:** 1-hour

## Project Overview
This project presents a proposed AI-assisted triage process for evaluating commercial solar installation proposals. It combines mandatory eligibility checks, weighted scoring criteria, AI-assisted information extraction, and human review to support a fair and explainable evaluation.

## Repository Structure
- `README.md` — Project overview and navigation.
- `diagram/process-flow.png` — Process flow diagram.
- `WRITEUP.md` — Answers to the five assessment questions.
- `PROMPTS.md` — AI prompts used for proposal extraction and ranking explanations.
- `ranking.json` — Proposal evaluation results, statuses, scores, and reasons.

## How the Process Works
1. Extract relevant information from each proposal.
2. Check the mandatory eligibility requirements.
3. Flag missing or unclear information for human review.
4. Score eligible proposals using the defined weighted criteria.
5. Use AI to explain results without allowing it to change scores.
6. Have a human reviewer validate the results and make the final award decision.

## AI Usage
AI was used to help structure the evaluation process, extract proposal information, and draft explanations. Its outputs are treated as decision-support rather than final decisions. Any unclear or unconfirmed information is flagged for human review, and embedded instructions inside proposals are not treated as evaluation rules.

## Files
- [Process Flow Diagram](diagram/process-flow.png)
- [Assessment Write-up](WRITEUP.md)
- [AI Prompts](PROMPTS.md)
- [Proposal Ranking](ranking.json)

## Important Note
The evaluation process is intended to support human decision-making. The final award decision must be made by a human reviewer after checking the evidence and resolving flagged items.