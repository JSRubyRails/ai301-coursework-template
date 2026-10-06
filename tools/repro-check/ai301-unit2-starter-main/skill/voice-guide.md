# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor learning how to work with an existing open-source codebase. I am using issue threads to claim work, reproduce reported problems, and contribute evidence before making changes. Readers can expect me to be specific about what I tested and honest about what I have and have not confirmed.

## Rules I write by

### Rule: State only what I know

I separate what I observed myself from what the issue reports. I do not present assumptions or untested explanations as facts.

- Wrong: "The parser is definitely broken because it cannot handle arrays."
- Right: "I reproduced the reported parser failure with a top-level JSON array."

### Rule: Include useful evidence

When reporting a reproduction result, I name the input, command, error, or other evidence that supports the result instead of only saying that something worked or failed.

- Wrong: "I tested this and got the same problem."
- Right: "Using a top-level JSON array as input produced the parser error described in the issue."

### Rule: Be clear about uncertainty

If I cannot reproduce something or have not tested part of the issue, I say so directly rather than guessing.

- Wrong: "This probably happens on every version."
- Right: "I reproduced this in the environment listed below; I have not tested other versions."

### Rule: Keep claims scoped to the issue

I describe the behavior relevant to the issue and avoid claiming that I found the cause or solution unless I have evidence for it.

- Wrong: "I found the bug and know exactly how to fix it."
- Right: "I reproduced the reported behavior and am investigating where the failure occurs."

### Rule: Make comments useful to the next contributor

I include enough concrete information for another contributor to understand what I did without filling the thread with unrelated detail.

- Wrong: "Claiming this. I'll look into it."
- Right: "I'd like to work on this issue. I'll first reproduce the top-level JSON array failure and document the environment and result."

## Things I never post

- A claim that I reproduced an issue without evidence supporting it.
- A promise about when I will finish the work.
- A guessed root cause presented as fact.
- A claim that a fix works before I have tested it.
- Vague comments such as "same issue" or "it doesn't work" without supporting context.
- Repository or environment details that I have not actually verified.
