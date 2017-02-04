# Models

This document describes how politicians, votes, etc. will be structured.

## Entities:
- Politicians: we want to trace back politicians' stances as far back as
  possible. Based off cursory exploration, there seems to be a distinct
  lack of digital records prior to 1996. This is to be expected. Working
  with what is currently available should be sufficient (20+ years of
  voting history, public statements, bill sponsorship should be enough).
  
  A possible complication in our data model is how we are going to store
  a politician's current role at a particular point in time. How their
  actions are processed is different if they have been elected to a legislative
  or executive role.

- Bills: bills are to be tracked by their name, tags, and legislature,
  who the signing executive was, and whether it was signed or vetoed.
  These are modelled similarly at the state and federal level (governor
  signs/vetoes state bills, president signs/vetoes federal bills).

- Votes: votes are tallied on a per-politician and per-bill basis. To
  clarify, we are noting that a particular politician voted a certain way
  on a certain bill.

- Sponsorship: this is technically metadata on bills. This has a greater
  weight on a politician's support of a given issue than their vote. To
  clarify, if a politician is the co-sponsor of a bill, this bears more
  significance than their vote (which is assumed to be "for").

- Statements of support or dissent: these are used in the overall
  aggregation of a politicians' support of a given issue. It is currently
  unclear how to quantify these (statements can be for or against, but
  there are degrees to this, given the ambiguity of language).
