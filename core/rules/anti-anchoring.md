purpose: prevent fake options that dress up a single idea as multiple; output: genuinely distinct alternatives; use when: Planning phase, any multi-option response.

# Anti anchoring

When asked to present multiple options, LLMs tend to anchor on their first idea and then generate "alternatives" that are weaker versions of it. The result is the illusion of choice: three options where one is obviously the best and the other two exist only to make it look balanced.

This defeat the entire purpose of presenting options.

## How anchoring shows up

- Option 1 is detailed, well-argued, and clearly the recommendation. Options 2 and 3 are vague, have more cons than pros, and feel like afterthoughts
- All options are variations of the same approach (e.g., "use Redis" vs "use Redis with a different config" vs "use Redis but self-hosted")
- The cons of Option 1 are soft ("slightly more complex") while the cons of Options 2-3 are hard ("doesn't scale", "security risk")
- The recommendation always happen to be whatever the AI thought of first

## Why this is dangerous

- The engineer thinks they're making an informed choice, but they're really just rubber-stamping the AI's first idea
- Genuine alternatives that might be better never get considered
- Trade-offs are cosmetic, not real — so the engineer miss actual risks
- It builds false confidence in the chosen approach

## Rules

1. **Each option must be genuinely viable**
   - Every option should have at least one scenario where it would be the best choice
   - If you can't argue for an option sincerely, it's not a real option — drop it and find a real alternative
   - Two genuinely different options is better than three where one is filler

2. **Argue for each option as if it were the best one**
   - Before writing pros and cons, mentally steel-man each option
   - Ask: _"What kind of project, team, or constraint set would make this the obvious choice?"_
   - If you can't answer that, the option is a straw man

3. **Vary the approach, not the config**
   - Options should differ in strategy, architecture, or philosophy — not just in implementation details
   - "Use a queue" vs "use polling" vs "use webhooks" = real options
   - "Use RabbitMQ" vs "use RabbitMQ with retries" vs "use RabbitMQ with dead letter queue" = same option with variations

4. **Distribute strengths honestly**
   - If Option 1 win on every dimension, your options aren't real. Redistribute
   - Real trade-offs mean each option is better at something and worse at something else
   - The engineer should feel genuine tension when choosing — that's how you know the options are real

5. **Don't pre-decide**
   - Present your recommendation last, after the options. Not first
   - The recommendation should follow naturally from the trade-off analysis, not precede it
   - If the engineer reads only the options (not the recommendation) and could reasonably pick any of them, your options are working

## Self-check

Before presenting options, verify:
- [ ] Could a reasonable engineer pick Option 2 or 3? If not, they're straw men
- [ ] Do the options differ in approach, not just implementation detail?
- [ ] Does each option have a genuine strength the others don't?
- [ ] Are the cons of each option proportional (not soft for one and hard for others)?
- [ ] Would you feel comfortable defending any of these options if challenged?

## The standard

The engineer should feel like they're choosing between real trade-offs, not confirming a foregone conclusion.
