# Universal Letter-Based Major System

## Overview

This system is a modification and generalization of the traditional **Major System** for converting decimal digits into memorable letters, words, names, and mnemonic images.

The traditional Major System is highly effective, but its mappings are fundamentally **phonetic**. Consequently, the interpretation of a letter depends on its pronunciation, and pronunciation varies between languages. A letter such as `C`, `G`, `J`, or `X` may therefore represent different sounds—and potentially different numbers—depending on the language and the word in which it occurs.

While trying to use the traditional Major System to build a PAO list, several practical limitations became apparent:

- the mapping remains strongly dependent on pronunciation, which may not provide an immediate and automatic anchor for non-native speakers;
- the system is historically optimized around pronunciation rules of particular languages, making direct cross-language reuse difficult;
- for PAO construction, phonetic anchoring may feel less deterministic than a direct letter-based mapping;
- building PAO Persons from two initials alone significantly restricts the available candidate pool, even for a 00–99 system;
- extending a system based on weaker or language-dependent anchors can become increasingly difficult to do consistently.

The system described here deliberately changes the assumptions of the traditional Major System and of PAO systems derived from it. It should not be regarded as universally superior to phonetic Major-System approaches. Instead, it is intended as an alternative architecture that may be easier to use where orthographic determinism, visual representation, extensibility, and cross-language portability are preferred.

---

## Mapping

The current proposed mapping is:

```text
Digit   Primary consonants   Optional vowel
-----   ------------------   --------------
0       S Z                  O
1       T D                  A
2       N M                  -
3       F G                  E
4       R Q                  -
5       V W                  U
6       X H                  -
7       C K                  I
8       P B                  -
9       L J                  Y
```

Or, in compact notation:

```text
0 = [S,Z] + [O]
1 = [T,D] + [A]
2 = [N,M]
3 = [F,G] + [E]
4 = [R,Q]
5 = [V,W] + [U]
6 = [X,H]
7 = [C,K] + [I]
8 = [P,B]
9 = [L,J] + [Y]
```

Its fundamental principle is:

> **Digits are associated with written Latin letters rather than with phonemes.**

The objective is not to reproduce the traditional Major System exactly, but to retain some of its useful mnemonic properties while creating a system that is more language-independent, orthographically deterministic and suitable for names, initials, PAO systems, identifiers, and other mnemonic encodings based on written Latin letters.

---

## Design Goals

### 1. Language independence

The mapping should depend as little as possible on pronunciation.

For example, the pronunciation of `C` varies considerably between languages and even between words within the same language. In this system:

> **C always represents the same digit because the mapping concerns the letter C, not the sound produced by C.**

The same principle applies to every other Latin letter.

This makes the system substantially more portable between languages using the Latin alphabet.

---

### 2. Latin alphabet as the common representation

The system operates on the standard 26-letter Latin alphabet:

`A–Z`

No language-specific characters or phonetic transcription are required.

Diacritics can, where necessary, be normalized to their underlying Latin letters according to a separate normalization rule.

---

### 3. Deterministic letter-to-number conversion

Every Latin letter belongs to exactly one numeric class.

Therefore the mapping:

`letter -> digit`

is deterministic.

A given letter never represents two different digits.

This makes it possible to convert arbitrary Latin-letter sequences into numeric representations without knowing how those sequences are pronounced.

---

### 4. Preserve useful Major System associations

The system does not discard Major-System associations unnecessarily.

Several traditional relationships remain useful because they are memorable independently of—or in addition to—their original phonetic justification.

Examples include:

- `S/Z -> 0`
- `T/D -> 1`
- `R -> 4`
- `P/B` as a pair

Other letter pairs preserve useful relationships based on visual similarity, historical relationship, common usage, or lexical balancing.

---

### 5. Balanced lexical productivity

A system intended for PAO and general mnemonic use should avoid assigning one digit only rare letters while another digit receives several highly productive letters.

The mapping therefore attempts to distribute useful Latin consonants reasonably evenly.

This is particularly important when generating 00–99 pegs. A poorly balanced system could make one combination extremely productive while making another unnecessarily difficult to represent with names or words.

The current mapping is optimized primarily with **English letter frequencies** in mind while retaining structural properties intended to make it usable with other Latin-alphabet languages.

Perfect statistical equality is neither possible nor necessary. The objective is reasonable lexical coverage without sacrificing stronger mnemonic relationships.

---

## Core Consonant Mapping

| Digit | Consonants |
| ----: | ---------- |
| **0** | S, Z       |
| **1** | T, D       |
| **2** | N, M       |
| **3** | F, G       |
| **4** | R, Q       |
| **5** | V, W       |
| **6** | H, X       |
| **7** | C, K       |
| **8** | P, B       |
| **9** | L, J       |

Every consonant of the basic Latin alphabet occurs exactly once.

---

## Rationale for the Consonant Groups

Not all pairs have the same origin. This is intentional: the system prioritizes useful structure over forcing every association to follow one artificial rule. The groups combine mnemonic relationships with lexical balancing.

### 0 — S/Z

This preserves the familiar Major-System relationship and creates a natural pair of closely related letters.

### 1 — T/D

T and D form an exceptionally useful pair and preserve one of the strongest relationships inherited from the traditional Major System.

They are also common letters, giving digit 1 strong lexical productivity.

### 2 — N/M

N and M are visually and structurally related letters and form a productive pair.

### 3 — F/G

This pair is primarily a balancing choice. It groups a stronger and a weaker lexical candidate while keeping the overall alphabet distribution useful.

### 4 — R/Q

This pair is also primarily a balancing choice.

R is highly productive, while Q is rare. Pairing them prevents Q from creating an excessively weak numeric class.

### 5 — V/W

V and W have a strong historical and visual relationship.

More importantly:

> **V is the Roman numeral for 5.**

This provides a strong direct mnemonic anchor for the group.

### 6 — X/H

X and H have historical and phonetic relationships in several languages, including transliteration traditions derived from Greek.

The relationship is not universal, but it provides a useful cross-linguistic association while allowing the relatively rare X to share a class with the much more productive H.

An additional optional mnemonic anchor may be the association of `hex-` with six.

### 7 — C/K

C and K have a strong orthographic and linguistic relationship across many Latin-alphabet languages.

Unlike a phonetic Major System, however, this system does not depend on how C is pronounced in a particular word:

> `C -> 7` always.

### 8 — P/B

P and B form a strong and familiar pair.

There is also a useful visual mnemonic:

> **B resembles 8.**

### 9 — L/J

L and J are visually similar, particularly in simple lowercase forms:

`l   j`

This provides a direct letter-shape association independent of pronunciation.

---

## Optional Vowel Layer

Vowels are handled differently from consonants.

They are **not ordinary members of the consonant groups**. Instead, they form a secondary mapping layer:

| Digit | Consonants | Optional vowel |
| ----: | ---------- | :------------: |
| **0** | S, Z       | O |
| **1** | T, D       | A |
| **2** | N, M       | — |
| **3** | F, G       | E |
| **4** | R, Q       | — |
| **5** | V, W       | U |
| **6** | X, H       | — |
| **7** | C, K       | I |
| **8** | P, B       | — |
| **9** | L, J       | Y |

For example:

```text
1 = [T,D] + [A]
```

This does **not** mean that A, T and D must behave identically in every application. It means that all three have the same numeric interpretation, while applications may decide which letters are significant for a particular encoding task.

---

## Encoding Modes

The letter-to-digit mapping itself never changes. What changes between applications is whether a given letter participates in a particular encoding.

### Strict / Explicit Letter Mode

Every significant written letter is interpreted according to the mapping, including mapped vowels.

This is the mode used by the PAO architecture described later in this document.

Examples:

```text
A -> 1
D -> 1
```

Therefore:

```text
AD -> 11
```

and consequently:

> **Albrecht Dürer -> AD -> 11**

This mode is particularly useful for personal names, fictional characters, initials, abbreviations, acronyms, identifiers, and PAO Persons.

### Flexible Word Mode

In mnemonic word construction, selected vowels may be treated as non-significant filler characters in order to increase lexical freedom and make mnemonic words easier to construct.

This does not change the underlying mapping. For example, `A` still has the unique numeric interpretation `1`; it is simply ignored when the encoding rule for a particular mnemonic word declares it non-significant.

This mode preserves one of the strongest practical features of the traditional Major System: the ability to use vowels freely when constructing pronounceable words.

---

## Complete Alphabet Coverage

When both consonant and vowel layers are considered, all 26 basic Latin letters have a unique numeric assignment:

```text
0 = S Z O
1 = T D A
2 = N M
3 = F G E
4 = R Q
5 = V W U
6 = X H
7 = C K I
8 = P B
9 = L J Y
```

No letter occurs in more than one class.

Consequently:

> **Every Latin letter has exactly one numeric interpretation.**

The distinction between Strict / Explicit Letter Mode and Flexible Word Mode concerns whether a letter participates in a specific encoding—not the numeric interpretation of the letter itself.

---

## Determinism

### Letter -> Number

This direction is deterministic.

For example:

```text
S -> 0
A -> 1
M -> 2
E -> 3
R -> 4
V -> 5
H -> 6
I -> 7
B -> 8
Y -> 9
```

No pronunciation information is required.

### Number -> Letter

This direction is intentionally one-to-many.

For example:

```text
8 -> P or B
```

and, where vowels are significant:

```text
1 -> T, D or A
```

This asymmetry is desirable. Deterministic letter-to-number conversion supports classification and decoding, while one-to-many reverse mapping provides lexical freedom for mnemonic construction.

---

## Relationship to the Traditional Major System

This system should not be considered a strict implementation of the classical Major System.

The classical system fundamentally maps:

```text
digit <-> phoneme
```

whereas this system maps:

```text
digit <-> Latin letter class
```

Its defining transformation is therefore:

> **phonetic encoding -> orthographic encoding**

This sacrifices some of the phonological elegance of the traditional Major System but removes one of its major sources of language dependence.

The resulting system is intended to preserve the practical mnemonic philosophy of Major rather than its exact phonetic implementation.

---

## Advantages

The resulting architecture provides several useful properties simultaneously:

1. **Language independence** — pronunciation is not required to determine a letter's numeric value.
2. **Latin-alphabet portability** — the same mapping can be used across languages employing the Latin alphabet.
3. **Deterministic decoding** — every letter maps to exactly one digit.
4. **Mnemonic compatibility** — several strong associations from the traditional Major System are retained.
5. **Balanced consonant coverage** — rare letters are generally paired with more productive letters rather than forming unusably weak classes.
6. **PAO suitability** — mapped vowels substantially increase the available space of names and initials.
7. **Traditional word-building flexibility** — Flexible Word Mode can preserve vowels as filler characters when needed.
8. **General-purpose applicability** — the system can encode words, initials, abbreviations, names, identifiers, and other Latin-letter sequences.

This mapping should currently be regarded as the **working specification** of the Universal Letter-Based Major System.

---