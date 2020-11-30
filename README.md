# Design Solution

The development process is design-driven. Significant changes to the architecture, features, or tools must be first discussed, and sometimes formally documented, before they can be implemented.
This document describes the process for proposing, documenting, and implementing changes to the organization.

* If you don't know what technology use, to solve your problem, there are two options:

1 - Make a POC (proof of concept) with your options and open a Pull Request asking for validation, in this case everybody decides together.

2 - Make the decision first, and submit the proposal to the group.

Before writing the design doc you can talk with others to evaluate what options you have talking about technologies solutions that are used and made before.

## The Design solution process

The Design Solution process is the process for reviewing a proposal and reaching a decision about whether to accept or decline the proposal and split the implementation in small waves.

 1. Open a specific branch to start write the Solution Design;
 2. The proposal author open a Pull Request and in this time start async discussion whith the team through the PR review.
 3. Schedule a Design Solution review meeting
 4. The PR is blocked until we have at least 2 approving reviews. At this time we consider Design Solution approved.

## Design Solution Documents

Design Solution Document will guide you to describe how the solution will be implemented and what kind of problem you are trying to fix.

 - The design doc should be checked in to specific feature/product repository as `designdocs/shortname.md`
 - The design doc should follow [the template](https://github.com/vbrazo/designdocs/blob/master/template.md)

## Design Solution Review meeting

The main goal of the review meeting is to make sure that Design Solutions are receiving attention from the right people, by cc'ing relevant developers, raising important questions, pinging lapsed discussions, and generally trying to guide the discussion toward agreement about the outcome. The discussion itself is expected to happen on the issue tracker so that anyone can take part.

The Design Solution review meetings also identify issues where consensus has been reached and the process can be advanced to the next step (by marking the proposal accepted or declined or by asking for a split design doc in more design solutions).  
