**Lexical Analysis**: Breaks down source code into tokens (each token or "category" defined by a regular expression) | characters → tokens
* **Token**: ```integer-literal = [-] (0…9) { 0…9 ∣ _ }```
  1. [] = optional
  2. a digit (0 through 9 denoted with 0…9) followed by
  3. { 0…9 | _ } denotes a repetition of 0 or more elements of 0…9 | _ .
* Lexeme: a string of a token

**Syntax Analysis**: Validate token sequences against a grammar and build a parse tree | characters → tokens → parse tree
* Lexical Analysis + (Parsing) groups the categories together to determine if they form a grammatically correct sequence
* Parsing is done according to a grammar

**Semantics**: What the parse tree means (types, scopes, variable/function use) | parse tree → meaning/correctness
```
DEFINITE_ARTICLE  NOUN  VERB  DEFINITE_ARTICLE  NOUN  PERIOD
```
* The milk drank the cat
* Parsing are the categories of words and not the specific words. The sentence above has the correct “look”, even though it does not make sense semantically.

## Lexical Analysis & Longest Matching Prefix

![](https://github.com/vickydee/midterms/blob/1bedc82c7f7bb760d0ca87d6f0126903a65940b5/Screenshot%202026-03-04%20114051.png)

**Longest Matching Prefix**: getToken() returns the longest prefix of the remaining input matching any token pattern.
* if an error is encountered, getToken() will advance one non-space character

**Tie-Breaker**: If the longest prefix matches multiple token types, the earlier token in the specification wins.

**Separators**: Whitespace or specific chars (e.g., &, !) force the lexer to stop and return the current longest match.


![](https://github.com/vickydee/midterms/blob/master/Screenshot%202026-03-04%20115236.png?raw=true)


**Ambiguous Grammar**: Exists a string has two different parse trees OR two different leftmost derivations OR two different rightmost derivations
Note: A leftmost derivation differing from its rightmost derivation does NOT imply ambiguity.
### Example (not ambiguous)

Grammar:

```
E → E + E | id
```

For the string:

```
id + id
```

Leftmost derivation:

```
E
E + E
id + E
id + id
```

Rightmost derivation:

```
E
E + E
E + id
id + id
```

### Example (ambiguous)

```
E → E + E | E * E | id
```

For the string:

```
id + id * id
```

Two different parse trees exist:


```
(id + id) * id
```


```
id + (id * id)
```

## 5. Top-Down & Predictive Parsing

### Top-Down Parsing
Start from the **start symbol** and expand downward to build the parse tree.

### Predictive Recursive Descent
* **No backtracking**
* The **next token (lookahead)** determines which rule to apply.

### Conditions for a Predictive Parser

For rules: `A → α` and `A → β`

Must satisfy: `FIRST(α) ∩ FIRST(β) = ∅`

Their FIRST sets **must not overlap**.

If: `A ⇒* ε`

Then: `FIRST(A) ∩ FOLLOW(A) = ∅`

If a symbol is **nullable**, its FIRST and FOLLOW sets must **not overlap**.

---

## 6. FIRST Sets

`FIRST(α)` = set of **terminals (and possibly ε)** that can begin strings derived from `α`.

### Rules

`FIRST(ε) = { ε }`

For terminal `a`: `FIRST(a) = { a }`

If: `A → Bα`

Then: `FIRST(B) − { ε } ⊆ FIRST(A)`

Add everything in `FIRST(B)` **except ε** to `FIRST(A)`.

If: `A → B₁ B₂ … Bₖ α` and `ε ∈ FIRST(B₁), … , ε ∈ FIRST(Bₖ)`

Then: `FIRST(α) − { ε } ⊆ FIRST(A)`

If: `A → B₁ B₂ … Bₖ` and **every** `FIRST(Bᵢ)` contains `ε`

Then: `ε ∈ FIRST(A)`

Add `ε` only if **A is nullable**.

---

## 7. FOLLOW Sets

`FOLLOW(A)` = terminals and `$` (end-of-input) that can appear **immediately after A**.

Important: `ε ∉ FOLLOW`

### Rules

Start symbol rule: `$ ∈ FOLLOW(S)`

If: `A → α B C`

Then: `FIRST(C) − { ε } ⊆ FOLLOW(B)`

If: `A → α B`

Then: `FOLLOW(A) ⊆ FOLLOW(B)`

If: `A → α B C` and `ε ∈ FIRST(C)`

Then: `FOLLOW(A) ⊆ FOLLOW(B)`

## HW 1

t1 = SUPPERID("supper22")

t2 = CRAZYID(”__crazy”)

t3 = ID("abc")

t4 = ID("_11")

t5 = ID("_11")

t6 = TI("abcd1e")

t7 = ID("abc")

t8 = ID("d1")

![](https://github.com/vickydee/midterms/blob/master/Screenshot%202026-03-04%20115325.png?raw=true)
