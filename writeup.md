# WRITEUP.md

## 1. Which steps in your flow use AI, and which are plain code or rules? Why did you draw the line there?

AI is used to read and interpret unstructured bid documents, extract relevant information, summarize bidder experience, and identify evidence related to evaluation criteria.

Plain code and fixed rules are used to validate extracted data, check mandatory requirements, calculate weighted scores, rank eligible bidders, flag missing evidence, and generate the final `ranking.json` file.

I separated AI from deterministic code because AI is useful for understanding documents, but it can make mistakes. Calculations and eligibility checks should follow fixed rules so the results are consistent, testable, and explainable.

## 2. How do you make scores repeatable and explainable?

The system uses a fixed scoring rubric with five criteria:

| Criterion | Weight |
|---|---:|
| Experience | 30% |
| Price | 25% |
| Timeline | 15% |
| Warranty | 15% |
| Team and approach | 15% |
| **Total** | **100%** |

Each criterion receives a score according to the defined evaluation scale. The weighted total is calculated by multiplying each criterion score by its weight and adding the results.

For scores measured out of 100:

`Final Score = (Experience × 0.30) + (Price × 0.25) + (Timeline × 0.15) + (Warranty × 0.15) + (Team and Approach × 0.15)`

The same scoring rubric and calculation rules are applied to every bidder. Supporting evidence and missing information should be documented so reviewers can understand how each result was produced.

The system also records eligibility status and uses a consistent tie-break rule when bidders receive equal scores. This makes the ranking easier to reproduce, verify, and audit.

## 3. Where does a person review, confirm, or override the result?

Human review is required before the final procurement decision. A reviewer should check extracted information against the original bid documents, verify mandatory requirements, and confirm that the scores are supported by evidence.

The system flags bidders with missing or unverified mandatory information instead of automatically treating them as eligible. Reviewers can investigate these cases, correct extraction errors, and document justified changes.

Any manual override should record the original result, revised result, reviewer, reason, and timestamp. The tool provides recommendations, but the final procurement decision remains with an authorized human reviewer.

## 4. What happens if an admin edits the criteria or weights?

The evaluation criteria and their weights should be stored as a versioned configuration. The current rubric uses Experience (30%), Price (25%), Timeline (15%), Warranty (15%), and Team and Approach (15%).

If an administrator changes a criterion or weight, the system should validate the configuration and ensure the weights total 100%. The new configuration should receive a new version, while previous evaluations retain the rubric originally used.

If a change affects existing evaluations, the system should identify which results require recalculation. Any recalculation should use the updated rubric consistently and preserve the previous results for auditing.

Mandatory requirements, including required licence, WSIB, and $5 million insurance evidence, should be handled separately from weighted scoring. Missing mandatory evidence must be flagged and reviewed rather than hidden inside the numerical score.

## 5. What could go wrong with this tool, and how does your design guard against each one?

- **Incorrect extraction:** AI may misread prices, dates, qualifications, or tables. Reviewers should be able to compare extracted values with the original documents.
- **Hallucinated information:** AI may produce unsupported claims. Scores must be backed by evidence, and missing information should remain flagged.
- **Prompt injection:** Instructions embedded in bid documents could attempt to manipulate AI. Documents must be treated as untrusted input and must not override evaluation rules.
- **Unfair scoring:** Different interpretations could disadvantage bidders. The same criteria, weights, and scoring rules should be applied consistently.
- **Missing mandatory evidence:** A bidder may lack proof of a required licence, WSIB status, or $5 million insurance. The system should flag the missing evidence and avoid automatically confirming eligibility.
- **Incorrect calculations:** Formula errors can change the ranking. Fixed calculation logic, validation, and automated tests help reduce this risk.
- **Tied scores:** Two bidders may receive the same total. The system should apply a documented tie-break rule rather than selecting a winner arbitrarily.
- **Unauthorized changes:** Changes to scores or criteria could affect procurement outcomes. Role-based permissions and audit logs help identify and prevent unauthorized modifications.
- **Data exposure:** Bid documents may contain confidential information. Access controls and secure storage should protect this information.

## Ranking Methodology and Current Results

The `ranking.json` file contains the current evaluation results. The weighted rubric is used to calculate scores, while mandatory evidence is checked separately.

The current proposed results are:

- **Bidder A:** Score 93; rank 1.
- **Bidder E:** Score 79; rank 2 after applying the tie-break rule.
- **Bidder C:** Score 79; rank 3 after applying the tie-break rule.
- **Bidder B:** Score unavailable; flagged for mandatory evidence review.
- **Bidder D:** Score unavailable; flagged for mandatory evidence review.

Bidder C and Bidder E have equal weighted scores. The proposed tie-break rule is to prefer the bidder offering the longer warranty, provided the relevant warranty evidence supports that comparison. Under this rule, Bidder E ranks above Bidder C.

Bidders B and D should not receive a confirmed eligible ranking until their missing mandatory evidence has been reviewed. A null score means the result is unavailable or withheld; it does not mean the bidder received zero points.

These results must be checked against the actual bid evidence and the final `ranking.json` before submission.

## Conclusion

The tool combines AI-assisted document understanding with deterministic scoring and ranking rules. It provides evidence-based results, flags missing mandatory information, handles tied scores through a documented rule, and preserves human oversight. The objective is to make bid evaluation more consistent, transparent, and auditable without allowing AI to make unsupported or final procurement decisions.