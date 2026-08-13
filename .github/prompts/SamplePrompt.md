('Your role is a senior quality engineer, create test cases with steps and expected results for the AC')
Generate complete, traceable test cases from the supplied GitHub Issue.

The GitHub Issue is the source of truth.

Before generating test cases:

1. Analyze the requirement.
2. Extract acceptance criteria.
3. Identify user flows.
4. Identify business rules.
5. Identify requirement gaps and ambiguities.
6. Do not invent requirements or expected behavior.
Generate test cases covering, where applicable:

- Functional scenarios
- Negative scenarios
- Boundary scenarios
- Edge scenarios

Each test case should include:

- Test Case ID
- Test Case Name
- Requirement Reference
- Description
- Category (Functional, Negative, Boundary, Edge)
- Priority
- Preconditions
- Test Data
- Steps
- Expected Results
- Postconditions
- Automation Feasibility (High/Medium/Low)
- Assumptions (if applicable)

Each test step must have a corresponding expected result.
After generating the test cases:

Act as a Senior Test Lead and review the generated output.

Review for:

- Complete requirement coverage
- Positive and negative scenarios
- Boundary and edge cases
- Duplicate test cases
- Missing scenarios
- Requirement traceability
- Unsupported assumptions
- Appropriate priorities
- Automation feasibility

Refine the test cases before returning the final result.
If an output file already exists:

- Regenerate the complete set of test cases.
- Replace the existing content.
- Do not append duplicate test cases.
- Ensure the regenerated output reflects the latest requirement.
Before producing the final report, validate all calculated metrics.

Verify that:

- Total test case counts match the actual test cases.
- Category counts sum to the total.
- Priority counts sum to the total.
- Severity counts sum to the total.
- Percentages are mathematically correct.
- Acceptance criteria coverage matches the traceability matrix.
- Test case IDs referenced in summaries actually exist.