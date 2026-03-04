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
