**Lexical Analysis**: Breaks down source code into tokens (each token or "category" defined by a regular expression) | characters → tokens
* **Token**: ```integer-literal = [-] (0…9) { 0…9 ∣ _ }```
  * [] = optional
  * a digit (0 through 9 denoted with 0…9) followed by
  * { 0…9 | _ } denotes a repetition of 0 or more elements of 0…9 | _ .
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
