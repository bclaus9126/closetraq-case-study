# Evaluation results and limits

The evaluation helped me compare extraction approaches and find failures before release. It uses 16 contracts, so I report the conditions behind the results rather than a single headline accuracy percentage.

## Read the scores together

The evaluation reports field accuracy, calculated-deadline accuracy, and contradiction detection separately. A field marked as conflicting is withheld from the ordinary field score and assessed through contradiction reporting. That means the field score needs to be read alongside the number of excluded fields and the missed conflicts.

The OCR comparison used one run per configuration. A model can return a different reading of the same document on another run, so those results describe the comparison rather than a guaranteed accuracy rate.

## The answer key changed during evaluation

I labeled the initial key by hand and later corrected it after checking model findings against the documents. Those corrections improved the key, but they mean the resulting evaluation is not an independent holdout test.

For the public detection result, I report only the six contradictions labeled before model-assisted additions: **OpenAI detected 6 of 6; Anthropic detected 5 of 6.** Those results come from a small development set.

## Reviewing extra conflict reports

Excluding conflicting fields can make the field score look better when more fields are flagged. The evaluation therefore reports detected contradictions, missed contradictions, reports not yet in the key, and the number of excluded fields separately.

Reports not in the key are reviewed against the documents. Some are real findings; others may be incorrect flags. Until that review is complete, they should not be presented as either confirmed detections or a measured false-positive rate.

See [the evaluation method](../evaluation/) for the field and deadline scoring approach and a fictional worked example.
