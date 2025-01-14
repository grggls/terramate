---
title: tm_substr - Functions - Configuration Language
description: |-
  The tm_substr function extracts a substring from a given string by offset and
  length.
---

# `tm_substr` Function

`tm_substr` extracts a substring from a given string by offset and (maximum) length.

```hcl
tm_substr(string, offset, length)
```

## Examples

```
tm_substr("hello world", 1, 4)
ello
```

The offset and length are both counted in _unicode characters_ rather than
bytes:

```
tm_substr("🤔🤷", 0, 1)
🤔
```

The offset index may be negative, in which case it is relative to the end of
the given string.  The length may be -1, in which case the remainder of the
string after the given offset will be returned.

```
tm_substr("hello world", -5, -1)
world
```

If the length is greater than the length of the string, the substring
will be the length of all remaining characters.

```
tm_substr("hello world", 6, 10)
world
```
