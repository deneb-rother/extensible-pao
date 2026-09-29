# Extensible PAO System

## Overview

A conventional PAO system ties numeric codes to **Person**, **Action**, and **Object** representations. The extensible architecture described here adds a hierarchical semantic layer intended to make the system easier to scale while preserving deterministic decoding.

The central principle is that the leftmost digits encode broader information, while additional digits narrow the identity of the Person.

Instead of encoding a Person exclusively from initials, the two-digit implementation uses:

```text
XY = Category(X) + PersonIdentifier(Y)
```

where the first digit identifies a semantic category and the second digit encodes the Person's surname or canonical identifying name according to the rules below.

For example, `4x` may represent Research, while the second digit identifies a particular scientist or explorer.

---

## Category + Identifier vs. Initials-Only Encoding

### Benefits

- **Semantic meaning of the code** — the first digit immediately provides information about the type of Person being recalled.
- **Reduced search space** — the category limits the search to roughly one tenth of the complete two-digit PAO set.
- **Semantic locality** — related Persons occupy the same numerical range.
- **Multiple retrieval paths** — a Person can be recalled through both category and name, providing partial redundancy and potentially improving error recovery.
- **Easier candidate selection** — candidates can be searched within a well-defined category using a single required name initial.
- **Natural hierarchical structure** — additional digits may progressively narrow identity rather than replace the meaning of preceding digits.
- **Graceful reduction** — a two-digit system can be reduced to ten major anchors represented by the categories.
- **Representation reuse** — the same real-world individual may potentially provide different canonical visual representations in different semantic roles, provided each representation is classified independently and remains visually distinct.

### Drawbacks

The principal cost is that decoding requires knowing something semantically important about the represented Person rather than relying on the name alone.

- categories require precise and operationally disjoint definitions;
- classification requires explicit rules;
- code derivation is less purely lexical than in an initials-only system because the canonical category must also be known and preserved across the system.

---

## Possible Hierarchical Extension Beyond Two Digits

The two-digit system described here is the current implementation. A longer Person code could preserve the same hierarchy.

For example:

```text
X    -> category
XY   -> category + canonical Person identifier
XYZ  -> category + canonical Person identifier + additional identifying component
```

In a three-digit implementation, the third digit could encode a first / second name (for multi word names) or the second letter of the name (in single word name cases). Additional digits should preserve the principle that leftmost digits carry broader information and rightmost digits progressively narrow identity.

The system should allow for an easy extension of the two-digit system, e.g. if William Shakespeare is coded as [10] then, assuming we use his first name initial as coding the third digit  - it would become [105] in the three-digit system; Robin Hood [24] would become [246]; Dracula [51] would become [514] etc.

The exact rules for `XYZ` and longer codes are implementation-specific and are intentionally left open here; the purpose is to show that the architecture can be extended without discarding the semantic meaning of existing prefixes.

---

## Category Mapping

The first digit is itself anchored through the Universal Letter-Based Major System by the first letter of the category label:

```text
0   [S]howbusiness
1   [A]rt
2   [M]yths
3   [G]raphics
4   [R]esearch
5   [U]nreal
6   [H]istory
7   [I]nventors
8   [P]layers
9   [L]iterature
```

The categories are **disjunctive within a PAO implementation**: every canonical visual representation must be assigned to exactly one category.

The classified entity is the **canonical visual representation**, not the complete biography of the underlying real or fictional individual.

This distinction is fundamental. A real person may have been an actor, athlete, politician, entrepreneur, or other public figure during their life. The PAO system classifies the specific representation being used. For example, an Arnold Schwarzenegger representation constructed as an actor or body builder belongs to Showbusiness and his political representation would belong to History. These are separate canonical representations, not simultaneous category memberships of one PAO Person.

---

## Category Definitions

- **showbusiness** — movie stars, actors, performers, singers, musicians; Persons primarily represented as performers of art;
- **art** — creators, composers, directors, painters, writers, photographers; Persons primarily represented as creators of art;
- **myths** — legends, deities, Greek heroes, folklore characters; human or human-like characters known from traditional or ancient tales;
- **graphics** — cartoons, anime, games; human or non-human characters whose canonical representation is primarily graphic or animated;
- **research** — scientists, explorers; Persons primarily associated with discovering, describing, or investigating something that exists;
- **unreal** — superheroes, fantasy and science-fiction characters that are non-human or superhuman and whose canonical representation is not primarily graphic nor mythological;
- **history** — rulers, politicians, and other real historical persons represented primarily through their historical or political identity;
- **inventors** — technologists, engineers, entrepreneurs, visionaries, industrialists; Persons primarily associated with creating technologies, systems, businesses, or other non-artistic constructs;
- **players** — athletes, sportspeople, team players, game players, chess masters; Persons represented through participation in sport or competitive play;
- **literature** — fictional human characters from novels, poems, film, television, or other narrative works, provided they do not belong to Myths, Graphics, or Unreal under the rules above.

---

## Representation-Based Classification Rules

Classification is **representation-based, not biography-based**.

When a canonical image could be interpreted in more than one way, classify what the image actually represents.

For example, a Superman-like image may potentially evoke Superman, Clark Kent, or Christopher Reeve. The correct classification depends on which identity remains encoded by the canonical representation. A representation constructed as Superman must be classified as Superman; it must not be placed in Showbusiness merely because Christopher Reeve supplied the face.

Similarly, a Person who has several real-world occupations should be classified according to the identity represented in the mnemonic image, not according to every occupation the individual ever had.

If a representation remains genuinely ambiguous between categories, the candidate should preferably be avoided or redesigned.

---

## Actor vs. Role Classification

Actor/role ambiguity is resolved through a visual test intended to be as objective as possible.

### Role

If the role remains recognizable after removing the actor's natural facial identity, the representation should be classified under the **role**.

In practice, this means that Costume and possibly Attribute provide sufficient identity without relying on the actor's Face.

Examples include highly characterized roles such as Jack Sparrow or Gandalf.

### Actor

If removing the actor's Face causes the role representation to lose its identity, the representation should be classified under the **actor**.

Examples include cases where the role is visually carried primarily by the actor's natural face rather than by independent characterization or costume. A scene showing Tom Hanks as Forrest Gump, Julia Roberts as Vivian Ward, Hugh Laurie as Gregory House, or David Schwimmer as Ross may therefore still encode the actor if the role cannot be identified without the actor's Face.

### Rationale

This rule serves two purposes:

1. it creates a deterministic visual criterion for actor-vs-role classification;
2. it prevents the Literature category from absorbing large numbers of visually actor-dependent roles while unnecessarily reducing the pool of usable actors in Showbusiness.

Boundary cases should be resolved consistently. If the role does not pass the face-removal test clearly, prefer the actor representation.

### Matrix Example

A Matrix-related representation illustrates the classification principle:

- **Keanu Reeves** as himself -> Showbusiness (`0x`);
- **Thomas Anderson** as an ordinary fictional human -> Literature (`9x`);
- **Neo** as the superhuman/unreal representation -> Unreal (`5x`).

This example shows how a given visualization should be classified. It does **not** imply that all three representations should necessarily be used simultaneously in one PAO set. Simultaneous reuse is acceptable only if the three canonical representations remain independently distinguishable.

---

# PAO Component Design

## Minimal Representation Principle

Every canonical PAO component should contain the **minimum amount of visual information required for reliable decoding**.

The design objective is:

> **Maximum semantic density with minimum frozen visual content.**

Unnecessary details make scenes more crowded, consume visual features that could otherwise remain available for Action or Object encoding, and increase the risk of interference.

The principle applies independently to Person, Object, and Action.

---

## Canonical Visual Representation

Every Person, Object, and Action should have a stable canonical representation.

A canonical representation defines the minimum visual features required to identify that component reliably within the current PAO set.

- Person: minimal Face / Costume / Attribute signature;
- Object: minimal shape / type / color / feature signature;
- Action: minimal movement, posture, relation, or instrument signature.

The goal is not photorealistic consistency. The goal is **stable decodability**.

---

## Person Rules

- Generic Person names such as `doctor`, `firefighter`, or `policeman` cannot be used as anchors. Such roles may still be used as visual elements of a named Person representation.
- The second digit follows this rule:
  - for categories **2, 3, and 5**, encode the first letter of the **canonical identifying name**;
  - for all other categories, encode the first letter of the **surname**.
- The canonical identifying name is the name under which the fictional, mythological, or unreal character is actually represented in the system, for example `Medusa`, `Shrek`, `Gandalf`, or `Neo`.
- Every Person must be recognizable through **exactly one or two** of the following identification channels:
  - **Face (F)** — facial structure, natural hair, beard, eyes, or other natural facial characteristics;
  - **Costume (C)** — clothing, makeup, artificial hairstyle, characterization, or other role-specific visual styling;
  - **Attribute (At)** — a stable identifying element such as a pipe, glasses, or hat.
- Use the **minimum sufficient combination**:
  - if `F` is sufficient, use `F` only;
  - if one channel is insufficient, add either `C` or `At`;
  - if `F + C` is still insufficient, do not automatically add `At`; instead, reconsider whether `C` is useful and whether `F + At` provides a cleaner representation;
  - if reliable identity requires `F + C + At`, the Person is usually too weak or too crowded and should preferably be replaced.
- Person-distinctiveness is evaluated **relative to the other Persons in the PAO set**, not in isolation.
- Frozen Person characteristics must not be transferred to other Persons.
- Frozen Person characteristics must not create an ambiguous decoding path with PAO Objects or Action attributes.

### Why the second digit assignement varies depenent on the person category

The distinction reflects how the two types of Persons are naturally identified. Real-world persons are typically distinguished by surname, while fantastic, mythological, and graphic characters are primarily recognized by their canonical identifying name. This preserves natural naming conventions while providing a consistent and scalable encoding rule.

### Why the two-feature maximum matters

If Tolkien is already reliably recognizable as an older man with a pipe, adding a distinctive coat may improve realism but does not improve the PAO architecture. It makes the canonical Person heavier, crowds future scenes, and freezes another visual feature unnecessarily.

The preferred representation is therefore the **smallest sufficient representation**, not the richest possible portrait.

---

## Object Rules

Three visually present object-like roles may exist in a canonical scene:

1. **Person Attribute** — a frozen identifying component of the Person;
2. **PAO Object** — the transferable Object encoded by the PAO slot;
3. **Action Attribute / Instrument** — a frozen element required to identify the Action.

### Person Attribute vs. PAO Object

An element belongs to the Person representation if removing it would make the intended Person substantially harder to identify and it is not selected as the transferable PAO Object.

This may include clothing element, body-related elements, or other visual attributes where appropriate.

Person Attributes are frozen and must not transfer to other Persons when PAO components are recombined.

The boundary between Person Attribute and PAO Object is ultimately implementation-dependent and relies on the strength of the user's visual associations.

### Object distinctiveness

Every PAO Object should be recognizable through **exactly one or two dominant properties**, selected from dimensions such as:

- distinct type (`ball`, `feather`, `bird`);
- distinct shape (`round`, `rectangular`, `branched`);
- distinct color where color is genuinely diagnostic;
- distinct structural feature (`engraving`, `spikes`, `holes`, `segments`).

If an Object requires many independent descriptive features to remain identifiable, it is usually too weak or too complex for a minimal PAO representation.

### Object transferability

Every Object must remain usable as a transferable token across different Actions and Persons.

An Action may move, deform, cover, rotate, enlarge, shrink, or otherwise interact with the Object, but enough of the Object's canonical identity must remain visible for reliable decoding.

### Visual part-whole exclusion

> **No PAO Object may be a visually identifiable part of another PAO Object already used in the system.**

The restriction is visual, not merely logical or anatomical.

For example, a heart may logically be part of a body, but it is not normally visible as a part of the body's external representation. By contrast, a hand is a visually identifiable part of a body. Using both `HAND` and `BODY` as separate Objects creates a transformational risk: an Action may partly obscure, crop, consume, or deform the body so that only the hand remains visible, making it difficult to determine which Object was originally encoded.

This rule protects Object identity under partial occlusion, cropping, deformation, and Action transfer.

---

## Action Rules

### Generic Actions are preferred

Actions should be as generic and transferable as possible.

An Action does **not** require a fixed instrument merely because real-world execution often involves one.

For example:

- `RIDING` can be defined as sitting astride the Object while moving;
- `SITTING` can be defined as sitting on the Object;
- `CUTTING` can be defined generically unless an instrument is needed to distinguish it from another Action.

In these cases, the transferred PAO Object itself occupies the relevant semantic role.

### Instrument-qualified Actions

An instrument may be frozen into the Action when it contributes meaningfully to Action identity or separates otherwise similar Actions.

Examples:

- `CUTTING WITH SCISSORS`
- `CUTTING WITH A RAZOR`
- `EXAMINING WITH A MAGNIFYING GLASS`
- `STABBING WITH A TRIDENT`

The instrument is then an **Action Attribute**, not the transferable PAO Object.

Instruments should not be introduced merely for realism. They should be used only when they improve discrimination or make the Action substantially clearer.

### Avoid independent secondary targets

Compound Actions that require an additional independent semantic object should generally be avoided, because they create ambiguity about which element is the transferable PAO Object.

The key distinction is not whether an Action uses something in the real world, but whether a fixed secondary element is required to understand the Action and competes with the PAO Object.

### Minimal Action representation

Each Action should be identifiable through **exactly one or two dominant features**:

- a distinct movement or relation (`catching`, `running`, `folding`, `slapping`);
- optionally, a distinct Action Attribute (`cutting with a razor`, `catching with a net`).

As with Persons and Objects, additional detail should be removed unless it is necessary for discrimination.

### Action transferability

> **An Action must remain visually identifiable when applied to Objects with substantially different geometry, material, scale, and semantic type.**

For example, a good generic Action should remain recognizable when transferred from its canonical Object to a cactus, ball, fish, stone, sheet, or machine.

The transferred scene may be physically impossible or absurd. Physical realism is secondary to deterministic visual decoding.

### Object identity preservation under Action

The Action may transform the Object, but should not erase the Object's canonical identity.

A transferred scene is valid only if both components remain recoverable:

```text
Action identity remains visible
AND
Object identity remains visible
```

---

## PAO Assignment Architecture

The two-digit code directly identifies only the Person:

```text
XY <-> P
```

Action and Object are not independently derived from `XY`.

The learned association architecture is:

```text
XY <-> P <-> O -> A
```

More explicitly:

```text
XY <-> P
P  -> O
O  -> P
O  -> A
```

The intended retrieval logic is therefore:

1. the numeric code identifies the Person;
2. the Person should strongly and naturally evoke the canonical Object;
3. once learned, the Object deterministically identifies its Person within the PAO set;
4. the Object evokes the canonical Action.

A direct Person-to-Action association:

```text
P -> A
```

is useful when present, but it is **not required**.

This is important because it allows the system to prioritize a strong `P -> O` association and a strong or learnable `O -> A` association without requiring the Action to be biographically characteristic of the Person.

The Object therefore acts as the central semantic bridge between Person and Action.


## Working Status

The Universal Letter-Based Major mapping and the two-digit Extensible PAO architecture should currently be regarded as a **working specification**.

The two-digit Person code, category system, canonical-representation rules, minimalism principle, transferability rules, and `P <-> O -> A` association architecture define the current implementation.

Longer Person codes (`XYZ...`) and PAOL are explicitly supported as architectural directions, but their detailed implementation may be refined independently without changing the core two-digit PAO model.
