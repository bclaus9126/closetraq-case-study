# Sending the PDF directly to the model

**Decision, September 2026:** remove the separate OCR step and send the contract PDF directly to the model. OCR converts page images into text before extraction.

## Why I tested it

The first version of CloseTraq sent OCR output to the model. During the rebuild, I wanted to know whether extraction errors came from the model or from information lost before it reached the model.

## The comparison

The evaluation used the same 16 contracts in four configurations: two providers, each with OCR text and with direct PDF input. Each configuration had one run. I compared the outputs against the answer key. The score below is the share of calculated deadlines that matched it.

| Provider | OCR text input | Direct PDF input |
| --- | --- | --- |
| Anthropic | 87.4% | 99.3% |
| OpenAI | 87.5% | 98.6% |

Direct PDF input improved deadline scores by roughly 11–12 percentage points for both providers in this comparison. Changing providers while retaining OCR changed the score by only 0.1 percentage point.

That pattern led me to inspect the document input rather than keep changing models.

## One failure that explained the decision

On one contract, both OCR-based runs reported the Effective Date as blank. Both direct-PDF runs captured the handwritten date on that line. The OCR output had omitted it, which affected six downstream deadlines.

Once the model received only the text, it had no image evidence to recover the missing date. Sending the PDF directly preserved information this workflow needed.

## Cost and tradeoff

The recorded mean extraction cost was $0.282 per contract with direct PDF input, compared with $0.182 through OCR. I accepted the additional ten cents per contract because of the improvement observed on this evaluation set.

## Limits

This was a comparison on 16 contracts with one run per configuration. It supported removing the separate OCR stage from this product; it does not establish that OCR is unsuitable for every document workflow or that either model has a particular production accuracy rate. Run-to-run variation and changes to the answer key also limit what these percentages can show. See [evaluation results and limits](4-evaluation-results-and-limits.md).
