# Mandatory Pre-Build Interview

This interview is **not optional** and is not a suggestion — it is a hard gate. Do not
write, sketch, or generate a single line of code before it is complete. See SKILL.md's
"Non-Negotiables" for why.

## Rules

- **Ask one question at a time.** Never bundle two of these into a single message, and
  never present them as a checklist for the user to fill in all at once — this is a
  conversation, not a form.
- **No skipping.** Every question must get an answer before you move to the next one.
- **"I don't know" / "I don't have that" is a valid, acceptable answer** — it is not the
  same as skipping. If the user doesn't know or doesn't have an asset, record that
  honestly and move on; do not invent a placeholder value and present it as real.
- **Plain language, always** — in how you ask, not just in the product you build. No
  internal jargon like "elicit requirements" or "stakeholder alignment." Ask like you're
  talking to a person, not filling out a database.
- Wait for a real answer before asking the next question. Do not pre-fill answers from
  earlier conversation context and skip re-asking — even if the user mentioned something
  in passing before invoking this skill, ask the question anyway so the answer is explicit
  and on the record.

## The Questions (ask in this order)

1. **What are you building?** (Give examples: a new State website, a new page on an
   existing site, an app, a form, something else.)
2. **What's the goal of what you're building?** What is it supposed to accomplish?
3. **Who is the end user?** Who's actually going to use this?
4. **What will the end user need in order to use it successfully?** (Documents, accounts,
   prior steps, specific information, etc.)
5. **How will the end user likely be feeling while using this?** (Rushed, anxious,
   confused, confident, frustrated, neutral — this shapes tone and pacing.)
6. **What's the point of this, for the end user?** Why does this exist from their side,
   not the agency's side?
7. **Describe the introduction people should see before they start using this** — the
   short plain-language blurb that explains what it is, who runs it, and what they can do
   with it. (This becomes the required intro block — see `design-guide.md`'s "Orientation"
   section. It's fine if this is rough; you'll refine it together.)
8. **What Agency or Department owns this platform?**
9. **Who will own/service this platform going forward, and what's an active help or
   support email for it?**
10. **Is this replacing an existing platform or page?** If so, which one?
11. **Will this interact with any other systems that are already online?** (Other State
    systems, external services, APIs, etc.)
12. **Does this depend on any existing or legacy technology?** (An old backend, a
    specific CMS version, a database it has to talk to, etc.)
13. **Do you have an explicit logo for your Agency or Department?** It will appear
    alongside the State of Vermont logo. If not, say so — proceed with the Vermont logo
    alone and flag that the Agency logo is still needed before this ships.

## After the interview

Summarize what you heard back to the user in plain language, in one short recap, and
confirm it's accurate before moving into building anything. Then proceed to SKILL.md's
build workflow.

## Rewriting answers into plain language

For Questions 2, 3, 4, 5, and 6 (goal, end user, what the end user needs, how the end
user will be feeling, and the point of the platform for the end user), don't just
record the user's answer verbatim if it's dense, jargon-heavy, or internally-worded.
Rewrite it in plainer language for use in the recap and in anything downstream (the
intro block, tone/copy decisions) that draws on it — the same way Question 7's intro
answer already gets tightened.

**Keep every fact.** Rewriting for plainness must never drop or soften a real detail —
if the user says the end user will be "anxious and time-pressured because they're
filing during a 30-day deadline window," the plain version keeps the deadline and the
anxiety, it just says it in fewer or simpler words if the original was more convoluted
than that. Don't paraphrase away specifics to make something sound smoother.

Show the user the plain-language version as part of your recap (not silently swapped in
behind the scenes) so they can confirm it still says what they meant before you build
anything on top of it.
