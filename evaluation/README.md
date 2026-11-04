# Evaluation method

I evaluate extraction at two levels: whether the model reads the contract fields correctly, and whether those readings produce the expected deadlines. Contradiction detection is tracked separately.

## The answer key

The initial key was labeled by hand from 16 signed Texas contracts in August 2026. Names and addresses in the key were replaced with stand-ins; dates, day counts, and amounts were retained because they affect the evaluation. The source contracts and real answer key are not published.

I later revised the key after checking model findings against the documents. The revised key is useful for development, but is not an independent holdout set. The public contradiction-detection result uses the six contradictions labeled before model-assisted additions. [Results and limits](../decisions/4-evaluation-results-and-limits.md) explains the distinction.

The worked example below uses fictional dates and day counts to illustrate the deadline check.

## Field and deadline scores

1. **Field score:** compare the extracted value with the labeled value, subject to the conflict exclusions described below.
2. **Deadline score:** pass the extracted values through the product's date calculations and compare the dates with the manually calculated key.

Both matter. A field-level error shows what was misread; a deadline-level error shows its effect on the timeline. Names are checked for presence only, because the private source documents contain real names while the key contains stand-ins.

## Checking the date calculations

The private tests recalculate expected deadlines from the labeled contract fields and compare them with the manually calculated dates. A mismatch requires checking both the code and the key against the document.

For example, these fictional inputs let me check several date calculations independently of the document reader:

| Input | Value | Expected result |
| --- | --- | --- |
| Effective Date and option-period length | October 19, 2026; seven days | October 26, 2026, at 5 p.m. local time |
| Effective Date and financing-approval period | October 19, 2026; 21 days | November 9, 2026 |
| Closing date and new-survey lead time | November 20, 2026; three days before closing | November 17, 2026 |

These examples illustrate selected calculations. They do not establish which terms apply to a particular transaction.

## Contradictions and excluded fields

| Reported count | Meaning |
| --- | --- |
| Found | A contradiction in the key that the model reported |
| Missed | A contradiction in the key that the model did not report |
| To review | A reported contradiction that is not in the key |
| Fields held | Fields excluded from the field score because the model flagged a conflict |

A conflicting field can be empty by design. The field score excludes it, while contradiction reporting records whether the conflict was detected. The excluded-field count is reported alongside the score so a smaller denominator remains visible.

"To review" is a review queue, not automatically a count of errors. I check those reports against the source documents before classifying them. This matters because flagging more fields could otherwise improve the field score simply by removing difficult cases from it.

## Consistent treatment of missing values

Absent values use `null`, with a separate reason such as blank on the form, not applicable, waived, no selection, or conflicting. The value and its absence reason are checked separately. Keeping value and reason separate avoids treating different prose descriptions of the same absence as different answers.

## Comparing runs

Each comparison uses the same contract set and records extraction cost, time, field score, deadline score, and contradiction counts. The [OCR comparison](../decisions/1-dropping-ocr.md) used two providers with both OCR text and direct PDF input, with one run per configuration.

This page documents the evaluation method. The source contracts, extraction prompts, scoring tools, application tests, and full answer key are kept private.
