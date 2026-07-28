# Recording a Product Walkthrough

Use this guide when recording a product area for AI evidence extraction.

The goal is not to create a polished demo. The goal is to make product behavior, context, conditions, and uncertainty visible.

## Before recording

Choose one bounded product area or flow. Avoid scopes such as “the whole ATS.” Prefer scopes such as “create, submit, and edit a recruitment request as the request owner.”

Prepare a safe account and enough representative data to demonstrate the flow. Hide personal data, credentials, tokens, private messages, and sensitive customer information.

## Start the recording with context

State these items aloud when known:

- Product and product area
- Goal of the walkthrough
- Actor and role
- Authentication state
- Account, plan, permission, or configuration that may affect behavior
- Environment, such as production or staging
- Starting point

Example:

> This walkthrough covers Recruitment Request in Cando ATS. I am logged in as the request owner in an account with an approval workflow. I will show creation, submission, and editing.

## While recording

- Say what you intend to do before an important action.
- Pause briefly after an action so the resulting state is visible.
- Explain important business rules, permissions, state changes, validation, persistence, and alternate outcomes.
- State conditions that may limit a behavior, such as a role, account type, workflow configuration, or current status.
- Distinguish what is visible from what you only know or remember.
- Say “I am not sure” when uncertain.
- Call out a possible bug as a possible bug, not as an intended rule.
- Mention relevant paths that are unavailable or that you intentionally skip.

Do not narrate every click or label. Focus on meaningful product behavior.

## Try to show

When relevant to the selected scope:

- Entry points
- Main flow and outcome
- Alternate paths
- State transitions
- Permissions and access gates
- Validation and error messages
- Cancellation
- Persistence after refresh or revisit
- Empty states
- Failure, fallback, and recovery
- Important shared-service behavior visible to the user

A single recording does not need to cover all of these. The final evidence package will state what was and was not covered.

## Safety

Stop or skip an action when it may:

- Delete or irreversibly change real data
- Publish or send a real message
- Charge money
- Change permissions or account configuration
- Expose sensitive data
- Affect another real user

Describe the untested behavior instead, and clearly state that it was not demonstrated.

## End the recording

Briefly state:

- What was covered
- What was narrated but not demonstrated
- What remains untested
- Where you were uncertain
- Which role, account, or state may need another recording

## Recording quality

- Keep text legible.
- Record the full relevant application window.
- Use clear audio.
- Avoid long unrelated pauses.
- Prefer multiple focused recordings over one very long recording.
