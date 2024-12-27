---
title: "Welsh Dictionary Sorting"
company: "Bloomberg"
category: "technical"
role: "new-grad"
date: "2024-11-21"
---

# Welsh Dictionary Sorting

## Question

There is a Welsh dictionary with an ordering of characters:

```
"a", "b", "c", "d", "dd", "e", "fh", "j", "i"
```

Note that each “character” in Welsh can be:

- A **single** English character, or
- A **double** (e.g., "dd", "fh").

When parsing words, you must give **priority** to the **double** character.  
For example, in `"ddb"`, the characters should be `["dd", "b"]`, **not** `["d", "d", "b"]`.

You are then given a list of words, e.g.:

```
["dae", "dde", "jia", "afhe"]
```

You need to **sort** the list of words according to the Welsh dictionary order and **return** the sorted list.

## Key Points to Consider

1. **Custom Character Order**: Must handle “dd,” “fh,” etc. as single units.
2. **Parsing Logic**: Ensure words are split correctly into Welsh characters.
3. **Sorting Algorithm**: Compare words lexicographically using the custom order.

## Possible Approaches

- Create a **mapping** from each Welsh character to its rank (0, 1, 2, …).
- **Convert** each word into a list of Welsh “tokens” before comparing.
- Use a standard sorting function with a **custom comparator** that respects the Welsh order.
