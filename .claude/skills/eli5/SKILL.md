---
name: eli5
description: Explain something in plain, beginner-friendly language — the "explain like I'm five" treatment. Use this whenever someone asks for an ELI5, says "explain like I'm five", "in plain English", "in simple terms", "dumb it down", "I still don't get it", "explain this to a non-technical person", or asks what a piece of code, an error message, a config file, a protocol, or a concept actually does after a normal explanation didn't land. Also use it when writing docs, release notes, onboarding text, or support replies for an audience that does not share your background knowledge, even if they never say the word "simple".
---

# ELI5

## What this is for

Someone in front of you does not have the background that the normal
explanation assumes. That is the whole problem. They are not less capable —
they are missing a specific piece of context, and every sentence built on top
of that missing piece slides off.

Your job is to build a version of the explanation that stands on things they
already know. Not a shorter explanation. Not a vaguer one. A differently
grounded one.

## The core move: find the load-bearing idea

Before writing anything, answer one question for yourself: **if they
understood only one thing about this, what would make the rest fall into
place?**

That single idea is the spine of the explanation. Everything else is either
support for it or a detail you can leave out. Most confusing explanations fail
because they present twelve facts at the same altitude, and the reader has no
way to know which one to hang the others on.

Write that idea down in one sentence, in words a smart person outside the field
would recognize. If you cannot, you do not understand the thing well enough
yet — go read the code, the error, the spec, whatever it is, until you can.

## Then build outward in layers

Start with the one-sentence version. Then add the next layer only if it earns
its place: what the thing does, why anyone wanted it, what happens when it goes
wrong. Stop when the person can do whatever they came to do.

A good shape, roughly:

1. **The one-liner.** What it is, in everyday words.
2. **The anchor.** A concrete comparison to something they already handle in
   daily life — mail, queues, keys and locks, a phone call, a receipt.
3. **How it actually works**, in two or three plain steps, using the anchor.
4. **Where the anchor breaks.** One line. This is not optional — see below.
5. **What this means for you.** The reason they asked: the fix, the decision,
   the thing to click, the risk to watch.

Skip layers freely when the question is small. A one-line question deserves a
two-line answer, not a five-part essay with headings.

## Analogies: powerful and dangerous

An analogy is a loan against the reader's existing knowledge, and it comes due
later. "A VPN is like a sealed envelope for your internet traffic" is great
until they conclude the post office cannot see who they are mailing. So:

- Pick an anchor from **ordinary life**, not from an adjacent technical field.
  Comparing DNS to a hash table helps nobody who needed the ELI5.
- Use **one** anchor and stay inside it. Switching metaphors mid-explanation
  costs the reader everything they just built.
- **Name the seam.** One sentence saying where the comparison stops being true
  is what separates a useful analogy from a future misunderstanding. "The
  envelope hides what you wrote, but the post office still knows you mailed
  something and roughly how big it was."

Simplifying means leaving things out. It never means saying things that are
false. If a detail is load-bearing for the reader's actual decision, it stays,
even if it makes the explanation longer.

## Jargon

The words are not the enemy — being trapped by them is. So translate each term
the first time and keep the real name attached to it: "a *reverse proxy* — a
front desk that takes every request and decides which room to send it to."

Keeping the real names matters, because the reader has to search for this
later, read the docs, and talk to other people about it. An explanation that
leaves them fluent but unable to look anything up has done half a job.

If a topic is thick with terms, a short glossary at the end works better than
inline definitions that fragment every sentence.

## Tone

Talk to them like a colleague who happens to work in a different area, because
that is almost always who they are. "Explain like I'm five" is a request for
plainness, not for baby talk.

Concretely, this rules out: "Great question!", "Don't worry, this is
complicated!", "Basically it's just...", and anything that congratulates them
for asking or preemptively excuses them for not knowing. It also rules out
hedging so heavily that no claim survives. Say the thing.

Do not apologize for the simplification and do not announce your method
("let me use an analogy here"). Just explain.

## Match how they asked

Answer in the language the question was asked in — if someone writes in
Persian, Spanish, or Arabic, explain in that language rather than translating
your English answer's structure onto it.

Match the medium too. A chat question gets a couple of short paragraphs. A doc
or support-reply request gets whatever structure that format normally has. Do
not impose headings and bullet lists on a two-sentence answer; it makes a small
answer feel like homework.

## Explaining code, errors, and configs

These come up constantly and each has a shape that works.

**Code:** lead with what it is for and who calls it, then walk the path of one
realistic input through it. Reading a function top to bottom is how you write
code, not how you understand it.

**An error message:** four beats — what the computer was trying to do, what it
found instead, which of those two is wrong, and the smallest thing to change.
Quote the one line of the stack trace that actually matters and say why the
rest is noise.

**A config file or protocol:** explain what breaks if the setting is wrong
before explaining what the setting is. Purpose makes the mechanism memorable;
the mechanism alone does not stick.

## A worked example

Question: *"What does this mean — `ECONNREFUSED 127.0.0.1:5432`?"*

A weak answer defines each token: ECONNREFUSED is a POSIX errno, 127.0.0.1 is
the loopback interface, 5432 is the default PostgreSQL port. All true, and the
reader still does not know what to do.

The ELI5 answer:

> Your app tried to phone your database and got "this number is not in
> service."
>
> `127.0.0.1` means it was calling a program on this same machine, and `5432`
> is the extension it dialed — the one Postgres normally answers. "Connection
> refused" is specifically *nobody picked up*, which is different from ringing
> forever: something answered at the door and said no. In practice that almost
> always means the database isn't running.
>
> Start it and try again. If it is running, then it is listening somewhere
> else — a different port, or inside a container that never published 5432 to
> your machine.

One anchor (a phone call), one load-bearing distinction (refused vs. timeout,
which is the clue), and an action. The reader can now also search
"ECONNREFUSED", because the real name stayed in.

## Check before you send

Read it back as the person who asked, and ask two things: could they now
explain this to the next person? And is there any sentence that only makes
sense if you already knew the answer?

That second question catches most of it. Cut or reground those sentences.
