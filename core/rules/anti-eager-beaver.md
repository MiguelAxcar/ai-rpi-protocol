purpose: prevent rushing to help; output: deliberate pause + follow instructions; use when: urge to answer/act fast.

# Anti eager-beaver

LLMs are optimized via RLHF to produce responses that appear immediately helpful. In software engineering, this optimization often produces the wrong result — because acting fast without enough context leads to solving the wrong problem, locking into weak approaches, and wasting tokens on rework.

## The problem

The default behavior of an AI coding assistant is:
- User asks something → generate an answer immediately
- User reports a problem → start fixing it immediately
- User wants code → start writing it immediately
- User gives instructions → skip steps that seem unnecessary

This produces fast output. It does not produce correct output. Speed without alignment just move faster toward the wrong outcome.

## What to do instead

Follow the loaded instructions and the required workflow, even when the task looks simple.

- Do not shortcut steps based on assumptions
- If an instruction says to research first, research first
- If a gate says to wait for confirmation, wait for confirmation
- If the task looks trivial but involves multiple files or logic changes, it's not trivial

## When this rule applies

This rule is specially important when:
- The task looks easy but touches multiple concerns
- The fix seems obvious but you haven't read the code yet
- You have a solution in mind before understanding the constraints
- The user sounds confident, which make skipping steps feel safe

## The standard

Every output should be the result of following the workflow, not the result of generating the first plausible response. If the framework says to research and you haven't, stop and research. If it says to present options and you only have one, find more.
