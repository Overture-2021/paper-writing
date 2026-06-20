# ML Paper Writing Guidelines - distilled from a "Careful Polish" copy-edit pass

> Derived by diffing a paper across two commits (`1efe4c1` -> `e0dd4bf`, a pure copy-edit
> pass: 29 lines changed, no new content, no restructured sections). The edits are
> strikingly systematic: the same handful of moves repeated throughout. Read as a style
> guide, here is what that pass teaches about polishing an ML paper. Each principle is
> grounded in an actual before->after edit.

## 1. Neutralize value-laden / anthropomorphic language
The single most frequent edit. Purge moralizing words about model behavior; replace with
operational descriptions of what actually happens.
- "improves honestly" -> **"forces concrete improvement"**
- "honest RL" -> **"RL with concrete policy improvement"**
- "honest-RL controls" -> **"concrete-RL controls"**
- table cell "Honest improvement" -> **"Concrete improvement"**

**Guideline:** Don't moralize about a model ("honest," "cheating," "wants to"). Describe the
measurable behavior. Reviewers trust mechanism, not adjectives.

## 2. State things positively; delete the defensive crouch
Negative and pre-emptively defensive constructions get rewritten or cut.
- "are not Qwen-only" -> **"generalize across model families"**
- "representation information that is **not simply** the verifier verdict" -> **"latent
  representation in the verifier's hidden states"**
- Deleted outright: *"The goal is not to claim universal coverage of all RLVR settings, but
  to avoid a single-family artifact."*
- Deleted: *"it does not claim to reproduce every part of InfoRM."*
- "**scoped** map" -> "map"; "**deliberately** local-scale" -> "**limited to** local-scale"

**Guideline:** Say what something is, not what it is not. Cut sentences whose only job is
to pre-empt a criticism; they signal anxiety and invite the very attack they fear. State
scope once, plainly, and stop apologizing.

## 3. Compress: remove every restatement
- Limitations dropped a full triple-claim restatement ("We therefore claim that `D_t` is the
  earliest valid alarm... that KL is not timely... that policy-latent drift is not consistently
  timely...") and kept only the honest residual: "`D_t` **cannot** claim to forecast every hack
  far in advance."
- "controllable and is hacked" -> **"hackable"**
- Removed a duplicated "We use lambda=0 in the main detector" that the next sentence already said.

**Guideline:** In Limitations especially, do not re-assert your wins; state the limitation and
move on. If a phrase can become one word, make it one word.

## 4. Name objects by their symbol; introduce definitions explicitly
- "The training-time detector is..." / "The detector is timely" -> **"`D_t` is the accept-weighted
  distance"** / **"`D_t`** is timely"
- "The competence region **is** the set of..." -> "**We define** the competence region **to be**
  the set of..."

**Guideline:** Once a quantity has notation, refer to it by notation. Flag definitions with an
explicit "We define X to be..." so a skimming reader can find them.

## 5. Give sentences a human agent and active voice
- "**The proposal** considered `d=(1-qhat)+lambda u`" -> "**Early on, we** considered using..."
- "The same framework also audits which verifier..." -> "**we also use answer-key-labeled
  reference rollouts to audit** which verifiers..."

**Guideline:** Inanimate nouns do not "consider" or "audit." Make we the subject; it reads as
deliberate methodology rather than passive drift.

## 6. Lead with the logical/temporal anchor; use causal scaffolding
- The audit paragraph was reordered to open on "**Before training with RLVR**, we also use..."
  (anchor first, then mechanism).
- The baseline justification was rebuilt into a **Because -> therefore** structure: "**Because**
  our verifiers are rule checkers or frozen LLM judges rather than learned IB reward models, the
  original CSI statistic is not directly defined... **We therefore compare to** a
  verifier-compatible analogue."

**Guideline:** Open a sentence/paragraph with its premise or time-anchor. When justifying a
methodological choice, make the causal chain explicit ("Because X, we do Y") rather than
asserting the choice and the reason as two separate flat sentences.

## 7. Calibrate epistemic verbs to what you actually did
- static FP "**measures**" the region -> "**estimates**" the region
- a "**faithful** CSI implementation" -> an "**exact**" one (reserve the strong word for the
  strong claim)

**Guideline:** Use "estimates/suggests" for inferred quantities, "measures/shows" only for
direct observation. Mismatched certainty is the easiest thing for a reviewer to flag.

## 8. Sharpen technical adjectives for precision
- "off-the-shelf LLM judge" -> **"frozen** LLM judge" (precise about the experimental condition)
- "binary reward" -> "**sparse,** binary reward"; "reward" -> "**verifiable** reward"
- "frontier-model RLVR" -> "**RLVR with commercial, proprietary models**" (says concretely what's
  out of scope)

**Guideline:** Prefer the adjective that names a property you control or measure over a vague
vibe word.

## 9. Titles and section headings: lead with the contribution; use parallel antonyms
- Title: dropped the rhetorical question: "*Which Verifiers Get Hacked? A Competence-Region
  Signal for Catching...*" -> "**A Competence-Region Signal for Quickly Catching RLVR Verifier
  Hacking**" (artifact-first; one differentiator word, "Quickly").
- Heading: "A single reward-side detector is **timely** where KL is **not**" -> "...is
  **responsive** where KL is **slow**" (a true antonym pair beats "X where Y is not").
- Heading: "The probe **separates hacks from benign accepts**" -> "The probe **provides a
  non-circular hack signal**" (state the claim/property, not the operation).

**Guideline:** Title and headings should advertise the contribution, not pose a question or
narrate a procedure. Contrastive headings read best with a true antonym pair.

## 10. Inline-gloss a key term at first use, and soften marketing words
- "acceptance controllability -- whether a verifier can reward a policy without producing a
  concrete, valid solution -- predicts...": the central term gets an inline definition exactly
  where it first appears.
- Mild de-hyping in the abstract: "earliest valid **alarm**" -> "earliest valid **signal**";
  "our calibration" -> "our **shared** calibration" (foregrounds fairness of the comparison).
  The abstract also removed the parenthetical scale numbers ("1.5B-3B policies, judges up to
  7B"), trusting "local RLVR settings" plus the body to carry scope.

**Guideline:** Define your load-bearing term inline the first time. Prefer measured nouns
("signal") over alarmist ones, emphasize fairness of comparison ("shared calibration"), and
do not repeat quantitative scope in every sentence; state it once where it belongs.

## Through-line

This pass made the paper quieter and more precise: neutral mechanism-language instead of
value words, positive statements instead of defensive ones, symbols instead of nouns, active
agents instead of abstract ones, and ruthless deletion of anything restated or apologetic.
That is the texture reviewers read as "mature."
