# Meaning, not paragraph numbers

**Decision, August 2026:** name extracted fields by the information they represent, rather than their position on a contract form.

## Why

The Texas Real Estate Commission (TREC) revises its forms, and provisions can move. Its [November 2020 update](https://www.trec.texas.gov/article/rules-and-contract-updates-november-commission-meeting) describes moving termination-option language from Paragraph 23 into Paragraph 5 for the forms introduced in 2021. The [current resale form](https://www.trec.texas.gov/forms/one-four-family-residential-contract-resale) places the termination option in Paragraph 5B.

A field named for an old paragraph can survive a form revision while no longer referring to the right information. Naming it for its meaning makes the intent clearer and reduces dependence on layout.

## How I applied the rule

- Field names describe the information, such as the option-period length, rather than a paragraph number.
- Extraction looks for the relevant contract language, including termination rights, cutoff times, and deadline-extension conditions.
- The extracted form number and revision date are retained with the deal.
- Extracted values retain source wording and page references for the agent to check.

This helps with form revisions, but does not make them automatic. A change to the substance of a rule still requires review, updated logic where needed, and tests.

## Keeping rule sources traceable

The holiday rules retain references to the statutory subsections incorporated by the contract. Those references let me trace each entry to its source and recheck it when the contract or statute changes. They are references to maintain, rather than a reason to assume the rule will never change.
