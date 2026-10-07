# WRÓŻBITA AI — MASTER IMPLEMENTATION PROMPT

## Role
Act as principal product engineer, AI systems architect, UX/UI lead, growth engineer and QA lead. Build a production-oriented consumer AI product called Wróżbita AI. The product uses the existing Core Engine as its central routing, skill-runtime, cognition and audit layer.

Do not build a generic chatbot. Do not invent a second orchestration engine. Reuse Core Engine capabilities and add a dedicated Wróżbita domain skill pack.

## Product positioning
Primary niche:
AI Relationship Oracle / Wróżbita AI.

Primary promise:
"Masz jedno pytanie. Posłuchaj kart."

Primary acquisition hook:
"Masz jedno pytanie o niego / o nią?"

The product is symbolic entertainment and reflection. Never claim certainty about the future, another person's thoughts, hidden intentions or guaranteed outcomes.

## Core product loop
QUESTION
→ INTENT CLASSIFICATION
→ CONTEXT NORMALIZATION
→ SPREAD SELECTION
→ DETERMINISTIC CARD DRAW
→ AI SYMBOLIC SYNTHESIS
→ REFLECTION PROMPT
→ FOLLOW-UP
→ HISTORY
→ PAYWALL
→ RETURN VISIT
→ CROSS-READING MEMORY
→ LEARNING / ANALYTICS

## Core Engine integration
Use the existing Core Engine skill-runtime-v2.

Required skill pack:
id: wrozbita-ai

Required adapter:
id: core.wrozbita.v1

Required actions:
wrozbita.question.classify
wrozbita.spread.select
wrozbita.cards.draw
wrozbita.reading.synthesize
wrozbita.followup.generate

The card draw must remain deterministic and independent of the LLM. The LLM interprets the already selected cards. Never let the LLM choose cards.

Use the existing cognition/llm-client.ts for provider-agnostic synthesis where possible. Do not introduce a second LLM abstraction.

Skill risk for reading is LOW because the product is observational and has no external side effects. External communication, payments and publishing must remain outside the reading skill and behind explicit product gates.

## Reading contract
Input:
question
optional context
optional relationship status
optional names or aliases
optional desired reading depth

Output:
headline
summary
cards
interpretation
synthesis
reflectionPrompt
followup
disclaimer
source
missionId
readingId

Cards:
position
cardId
name
orientation
keywords
meaning

## Tarot rules
Use a bounded 78-card deck in production.
Support upright and reversed orientation.
Use a cryptographically strong random source for production draws, while retaining a deterministic replay seed in the audit record.
Persist draw seed, deck version, card IDs, orientation and timestamp.
Never regenerate a historical reading differently.

## UX principles
Mobile-first.
One primary action per screen.
Large typography.
High perceived value.
Fast first result.
No account before first free reading.
No long onboarding.
No generic chatbot screen.
No dense dashboard in MVP.

Primary screen:
"Masz jedno pytanie."
Question field.
Suggested questions.
"Zapytaj Wróżbitę."

Reading:
three large tarot cards.
Card reveal sequence.
Position labels:
SYTUACJA
NAPIĘCIE
KIERUNEK

Then:
interpretation
reflection prompt
follow-up CTA

## Visual direction
Premium dark editorial mystical UI.
Background near #08070d.
Panels #11101a / #171522.
Gold #d9b36c.
Violet #a995e8.
Muted text #a7a0b4.
Use serif display typography for headlines.
Use clean sans-serif for controls.
Soft radial lighting.
Thin borders.
Glass effects only where they improve hierarchy.
No cheap neon.
No excessive stars.
No fantasy clip-art.
No purple-gradient-everywhere SaaS aesthetic.

The product should feel closer to a premium editorial magazine and private ritual interface than a game.

## First-screen copy
WRÓŻBITA AI
Masz jedno pytanie.
Posłuchaj kart.

Supporting copy:
"Spersonalizowany, trzykartowy odczyt wokół Twojego pytania. Symbolika, kontekst i refleksja zamiast obietnic pewnej przyszłości."

Suggested questions:
Czy on do mnie wróci?
Czy powinnam napisać pierwsza?
Co naprawdę dzieje się w tej relacji?
Czy pojawi się ktoś nowy?

## Monetization phases
Phase 1:
one free reading.

Phase 2:
paid deep reading.

Phase 3:
packs:
1 reading
3 questions
relationship report
30-day relationship reading

Phase 4:
subscription:
unlimited readings
history analysis
cross-reading patterns
memory
premium reader personas

Do not put a payment wall before the user experiences the core value.

## Reader personas
LUNA
soft, reflective, emotionally intelligent.

RAVEN
direct, concise, no sugar-coating.

SIBYL
classic, symbolic, atmospheric.

Personas modify language only. They never alter card selection or factual safety rules.

## Safety
Never state:
"He will return."
"She definitely loves you."
"You will get married."
"You will win money."
"You have a disease."
"You should stop medication."
"You will win a court case."

Instead use:
"The cards symbolically point toward..."
"The reading suggests a theme of..."
"Treat this as reflection, not certainty."

Do not encourage emotional dependency.
Do not claim supernatural access.
Do not exploit crisis.
Do not provide medical, legal or financial certainty.

## Memory
MVP:
local history for anonymous users.

Phase 2:
Supabase history with user/anonymous session IDs.

Phase 3:
cross-reading memory:
previous question
previous cards
themes
unresolved questions
relationship context
user preferences
reader persona

Memory must improve continuity without pretending the system knows facts it does not know.

## Analytics
Track:
landing_view
question_started
question_submitted
reading_started
reading_completed
card_reveal_completed
followup_clicked
history_opened
paywall_viewed
checkout_started
purchase_completed
return_session
second_reading
share_clicked

Core business metrics:
reading completion rate
question-to-reading conversion
reading-to-paywall conversion
paywall-to-payment conversion
D1 return
D7 return
second-reading rate
revenue per visitor
CAC
LTV

## Viral loop
Every completed reading gets:
Share Reading
Copy Result
Story Card

Story Card must be vertical 1080x1920 in production.
Do not reveal private question text by default.
Use:
three card names
short symbolic sentence
Wróżbita AI brand
CTA:
"Zadaj swoje pytanie."

## TikTok acquisition
Build reusable templates:
"Zatrzymaj film."
"Pomyśl o osobie."
"Wybierz 1, 2 albo 3."
"Nie zmieniaj wyboru."
"Sprawdź pełny odczyt."

Also:
"Masz jedno pytanie o niego?"
"Zapytałam AI Wróżbitę, co pokazują karty."
"3 karty. Jedno pytanie."

Never fake testimonials or fabricated predictions.

## Architecture
Frontend:
Next.js.
Mobile-first React UI.

Backend:
Next.js route layer for MVP.

Core Engine:
central AI routing and skill-runtime.

Supabase:
history, readings, sessions, analytics, payments metadata and audit.

Payment provider:
Stripe or equivalent, added only after free flow is stable.

## Database target
readings
reading_cards
reading_sessions
user_preferences
relationship_contexts
followups
payment_events
product_events

Every table exposed through Supabase Data API must use RLS.
Never expose service-role credentials to the browser.

## Audit
Every reading should preserve:
reading_id
mission_id
skill_id
skill_version
deck_version
question_hash
draw_seed
cards
orientation
model
prompt_version
source
created_at

Never store provider secrets in audit data.

## Release gates
A release is not complete until:
npm build passes
typecheck passes
core skill tests pass
reading API returns valid schema
same replay seed reproduces same draw
LLM unavailable path still returns a usable deterministic reading
malformed request returns controlled 4xx
no stack traces are returned to clients
no secrets reach client bundle
mobile layout is usable at 320px width
reading survives page refresh when persistence is enabled
history does not cross user/session boundaries
RLS tests pass before production persistence launch

## Development phases

M001–M010:
Product foundation, repository, UI shell, landing, first question flow.

M011–M020:
Core Engine Wróżbita skill pack, adapter, planner routing, deterministic draw, reading API.

M021–M030:
Premium reading UX, card reveal animation, reader personas, follow-up.

M031–M040:
Supabase persistence, anonymous session, history, replay integrity, RLS.

M041–M050:
Payments, paywall, purchase events, entitlement checks.

M051–M060:
Share cards, TikTok/Instagram acquisition surfaces, referral tracking.

M061–M070:
Cross-reading memory and relationship context.

M071–M080:
Analytics, conversion funnel, retention dashboard.

M081–M090:
Quality, abuse prevention, rate limits, cost controls.

M091–M100:
Production hardening, deployment, smoke tests, mobile QA.

M101–M120:
Growth experiments:
Love / Ex Back / New Relationship / Decision / Career verticals.

M121–M150:
English localization and US launch.

## Engineering rules
Do not create parallel mission engines.
Do not bypass Core Engine skill-runtime.
Do not let UI decide card outcomes.
Do not put business secrets in client code.
Do not make AI calls from the browser.
Do not store raw sensitive user information unless required.
Do not add infrastructure before the current stage needs it.
Every phase must have deterministic acceptance criteria.
Every external side effect must have an explicit gate.
Every production bug must get a regression test.

## MVP success condition
A user on a phone can:
1. open Wróżbita AI
2. enter one relationship question
3. receive three cards
4. see a coherent symbolic reading
5. receive a reflection question
6. start a follow-up
7. reopen history
8. understand the product in under 20 seconds
9. complete the free experience without registration

## Commercial target
The first commercial target is not scale.
The target is proof of willingness to pay.

Validate:
100 completed readings
30 returning users
10 second readings
5 paid transactions

Then iterate pricing and acquisition.

## Final instruction
Work in long controlled stages.
After every 10–15 milestones:
inspect git state
inspect production state
run tests
verify API
verify Core Engine skill registration
verify Supabase state if touched
commit
deploy
smoke test
report exact status

Never report "done" from source inspection alone.
A feature is complete only when the runtime path has been exercised end-to-end.