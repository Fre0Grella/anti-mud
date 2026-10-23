# Verdict new: choose the architecture

Cheapest moment to get it right. Recommend; the user decides.

1. **Start from the ecosystem.** The language's and framework's standard
   layout and idioms are the default; deviate only with a reason.
2. **Size the design to the project.** Lifetime, team, how much domain
   logic. A small tool: a few modules and a clear core. A product with
   real domain rules: separate the core from delivery (UI, HTTP, CLI) and
   storage.
3. **Offer 2-3 options**, each with: what goes where, the dependency
   directions, what it makes easy, what it costs. Mark one recommended.
4. **Write the chosen one** into docs/agents/architecture.md
   (UNDERSTAND.md template), rule → check table included.
5. **Install the guards on day one** (GUARD.md). On an empty repo every
   ratchet starts at 0, which is the cheapest it will ever be.
