Q1. Which steps in your flow use AI, and which are plain code or rules? Why did you draw the line there?

Answer:AI is used to extract information from contractor proposals, identify relevant evidence, flag suspicious instructions, and generate short explanations for rankings. Plain code handles file validation, mandatory pass/fail checks, budget and timeline validation, weighted score calculations, and ranking. AI is useful for understanding unstructured documents, while code is more reliable for consistent calculations and fixed business rules. A human reviews uncertain information and makes the final award decision.

Q2. How do you make scores repeatable and explainable? If the same proposals were ranked twice, would the result be the same? How would a reviewer see why a proposal ranked where it did?

Answer:I would use fixed scoring formulas, configurable criteria weights, and consistent rules for every proposal. The system would save extracted facts, supporting evidence, scoring results, criteria versions, and the AI model and prompt versions used. Numerical scores would be calculated by code, with predefined tie-breaking rules, so the same inputs and configuration produce the same ranking. Reviewers could see each criterion's score, its contribution to the total, supporting evidence, and the reason for the final position.

Q3. Where does a person review, confirm or override the result? What gets logged for audit?

Answer:A reviewer selects the project category, uploads proposals, and checks flagged or uncertain information. After scoring, the reviewer examines the ranking and supporting evidence, corrects extraction errors, or overrides a recommendation with a written reason. The final award decision remains with an authorised human. The audit log records proposal identifiers, extracted facts, criteria and prompt versions, scores, flags, reviewer corrections, override reasons, timestamps, and the final decision.

Q4. What happens if an admin edits the criteria or weights after some proposals have already been scored?

Answer:The system would create a new version of the criteria instead of overwriting the previous version. Existing results would retain the configuration used when they were originally scored. If the admin changes the weights, the reviewer can request rescoring using the new version. The system would recalculate the scores, produce an updated ranking, and record the change. All weights must total 100%, and the original and revised results must remain distinguishable for audit purposes.

Q5. What could go wrong with this tool, and how does your design guard against each one?

Answer:PDF extraction may be incorrect, so the system preserves supporting evidence and allows human verification. AI may invent missing information; therefore, unknown facts are recorded as missing rather than guessed. Prompt injection is handled by treating proposal text as untrusted data and ignoring embedded instructions, such as the instruction in Proposal C to rank it first. Bias and inconsistent scoring are reduced through common criteria and fixed formulas. Missing mandatory evidence is flagged instead of automatically passed. AI costs are controlled by limiting unnecessary calls and reusing validated results where appropriate. Access controls and audit logs help prevent unauthorised changes, and secure storage protects proposal documents.
