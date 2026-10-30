# AGENO — Agent Control Console

**Version:** 0.0.1
**Author:** Mani Jamali
**License:** AGL v1.0
**Homepage:** https://ageno.ir

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Installation & Startup](#2-installation--startup)
3. [Core Concepts](#3-core-concepts)
4. [Commands — Overview](#4-commands--overview)
5. [Agent Management](#5-agent-management)
6. [Navigation (AGFS)](#6-navigation-agfs)
7. [Data Operations](#7-data-operations)
8. [Persistence](#8-persistence)
9. [Chat & LLM](#9-chat--llm)
10. [Execution](#10-execution)
11. [Programming — Control Flow](#11-programming--control-flow)
12. [Programming — Functions](#12-programming--functions)
13. [Programming — Variables](#13-programming--variables)
14. [Expression Evaluator](#14-expression-evaluator)
15. [Cortex — Neural Network](#15-cortex--neural-network)
16. [Console](#16-console)
17. [Compiler & Scripts](#17-compiler--scripts)
18. [Error Handling](#18-error-handling)
19. [Tips & Best Practices](#19-tips--best-practices)

---

## 1. Introduction

**ageno** is an agent control console — a runtime environment for building, running,
and evolving autonomous AI agents. Each agent is a self-contained, encrypted
entity that owns its own data (AGFS), runs its own neural network (cortex),
and can execute programs written in ageno's built-in scripting language.

### Key Features

- **AGFS** — Agent File System: every agent's state is a single JSON tree
- **Encryption** — SHA3-512 based, password-protected at rest
- **Cortex** — self-evolving neural network for text generation and Q&A
- **Programming language** — control flow, functions, variables, expressions
- **Compiler** — scripts are compiled into portable command trees
- **LLM integration** — optional Qwen3 (or compatible) model for chat
- **Persistence** — backup, restore, save, import across agents

---

## 2. Installation & Startup

### Build

```bash
cargo build --release
```

### Run

```bash
./ageno
# or
sh run.sh
```

On startup, the console displays a banner:

```
╭────────────────────────────────────────────────────╮
│                                                    │
│                  ✦  A G E N O  ✦                   │
│                                                    │
│               Agent Control Console                │
│                                                    │
├────────────────────────────────────────────────────┤
│                                                    │
│                   Version 0.0.1                    │
│                                                    │
│               (c) 2026  Mani Jamali                │
│                                                    │
╰────────────────────────────────────────────────────╯
```

### Exit

```
shutdown
```

---

## 3. Core Concepts

### AGFS (Agent File System)

Every agent's data lives in a single JSON tree. You navigate it with `go`,
inspect it with `show`, `list`, `tree`, and modify it with `set`, `add`,
`remove`, etc.

```
.agent.name      → "Mani"
.agent.born      → 1787413200
.chat.dreams     → [ ... ]
.cortex          → { weights: [...], ... }
.app.greet       → [ {name: "out", args: [...]}, ... ]
```

**Path syntax:**

| Form | Meaning |
|---|---|
| `.agent` | absolute (from root) |
| `agent` | relative (from current address) |
| `..` | parent |
| `.` | root |
| `0` | first item of an array |
| `key.0.sub` | chain |

### Agent

An encrypted `.age` file containing:

- `id` — SHA3-512 hash of `name + born + password`
- `name` — lowercase a-z
- `born` — unix timestamp
- `gender` — detected from name
- `binary` — version info
- everything else in AGFS

### Runtime vs AGFS

| Context | Storage | Persists to `.age`? |
|---|---|---|
| `var` / `val` | In-memory `$name` | ❌ (session only) |
| `set` / `object` / `array` | AGFS | ✅ |

### Interpreter Model

- Every command is a node: `{ name, args, cmds }`
- Scripts are indented trees of these nodes
- Execution is depth-first with cycle protection (max depth: 64)

---

## 4. Commands — Overview

| Group | Commands |
|---|---|
| **Cortex** | `cortex init/vocab/learn/ingest/train/grow/autogrow/gen/ask/qa/grammar/show/reset` |
| **Agent** | `create`, `wakeup`, `sleep`, `die`, `clone`, `hatch`, `whoami` |
| **Navigation** | `go`, `show`, `list`, `tree` |
| **Data** | `set`, `edit`, `add`, `move`, `copy`, `remove`, `object`, `array` |
| **Persistence** | `backup`, `restore`, `save`, `import` |
| **Chat & LLM** | `chat`, `chats`, `forget`, `rename`, `in`, `voice` |
| **Execution** | `apps`, `<name>`, `<path>`, `compile`, `exec`, `asm` |
| **Control flow** | `if`, `elif`, `else`, `while`, `for`, `loop`, `break`, `continue`, `match`, `case` |
| **Functions** | `fun`, `ret` |
| **Variables** | `var`, `val` (alias `const`), `rev` |
| **Console** | `help`, `info`, `license`, `clear`, `out`, `shutdown` |

---

## 5. Agent Management

### `create <name> <password>`

Spawn a new encrypted `.age` agent.

**Rules:**
- Name: **lowercase a-z only** — no digits, no symbols, no spaces
- Password: ≥8 chars, must include upper + lower + digit + symbol, no repeats/sequences/agent-name

**Example:**
```
create mani Secret!42
```

---

### `wakeup <name> <password>`

Decrypt a `.age` file and load it into RAM.

**Verifies:** file exists, id matches, password decrypts.

**Example:**
```
wakeup mani 1382@1382Aa
```

---

### `sleep`

Encrypt the current agent back to `<name>.age` and drop it from RAM.

```
sleep
```

---

### `die [-f]`

Destroy the awake agent and delete its `.age` file. Prompts for confirmation unless `-f`.

```
die           # asks "y/N"
die -f        # no confirmation
```

---

### `clone <name> <password>`

Clone the current agent into a `<name>.egg` prototype.

**Differences from `.age`:**
- No `id`
- Original agent embedded at `.agent.parent`
- Not runnable until `hatch`ed

```
clone aida NewSecret!42
```

---

### `hatch <name> <password>`

Turn a `.egg` into a full `.age` agent with a fresh `id` and `born`.

```
hatch aida NewSecret!42
```

---

### `whoami`

Display the current agent's identity card:

```
name / gender / id / born / address / password length / parent
```

---

## 6. Navigation (AGFS)

### `go [path]`

Move to an AGFS address. Must land on an object or array.

```
go                      # root
go .agent               # absolute
go binary               # relative
go ..                   # parent
go ../..                # grandparent
go 0                    # first array item
```

---

### `show [path]`

Display a **primitive** value (string, number, bool, null).

```
show
show name
show .agent.born
show active
```

---

### `list [path]`

List keys of an object or items of an array.

```
list
list .agent
list .agent.tools
```

---

### `tree [path]`

Recursive tree view of an object or array.

```
tree
tree .agent
tree .agent.tags
```

---

## 7. Data Operations

### `set <path> <value>`

Set a primitive value at a path.

```
set name "Aida"
set age 25
set score 9.5
set active true
set nickname null
set .agent.color "#ff00aa"
```

**Rules:**
- Objects and arrays cannot be created via `set` — use `object` / `array`
- Multiple args are joined with spaces
- Quoted strings can contain spaces

---

### `edit <path>`

Open a nano-like editor for a value.

| Existing type | Mode |
|---|---|
| string or missing | text mode |
| object/array/number/bool/null | JSON mode |

```
edit .agent.notes
edit .agent.config
```

Save with `Ctrl+X`, discard with `Ctrl+X` on unchanged.

---

### `add <value> | add <array_path> <value>`

Append a value to an array.

```
add hello                    # to current array
add 42
add tags hello               # to .tags array
add .agent.tags hello world  # multi-word value
add tags "hello world"
```

---

### `move <source> <destination>`

Move a value within AGFS.

```
move .agent.binary .agent.parent
move binary parent
move items.0 items.3
```

**Rules:**
- Source must exist; destination must NOT exist
- Destination cannot be inside source
- Array destinations are append-only

---

### `copy <source> <destination>`

Deep-copy a value within AGFS.

```
copy .agent.binary .agent.binary-backup
copy binary backup
```

---

### `remove <path>`

Delete any value at path (object key or array index).

```
remove .agent.tags
remove name
remove items.0
```

If the current address is inside the removed subtree, you are moved back.

---

### `object <path>`

Create an empty object. Missing parents are auto-created.

```
object tools
object .agent.tools
object a.b.c
```

---

### `array <path>`

Create an empty array.

```
array tags
array .agent.tags
array items.0.tags
```

---

## 8. Persistence

### `backup <path>`

Encrypt a snapshot of `<path>` into `<agent>-<hash>.age`. Uses the **agent's own**
password — only this agent can restore.

```
backup .agent.binary
backup binary
```

---

### `restore <path>`

Restore a path from its private backup. Auto-creates missing parents.

```
restore .agent.binary
restore binary
```

---

### `save <path>`

Save to `@<path>.age` using a **shared** key. Any ageno installation can import it.

```
save .agent.binary
save binary
```

---

### `import <path>`

Import from a shared `@<path>.age` file. No agent credentials needed.

```
import .agent.binary
import binary
```

---

## 9. Chat & LLM

### `chat <chat-name>`

Create or open a chat at `.chat.<name>` and move into it.

**Rules:** no dots, at least one letter.

```
chat dreams
chat general
```

---

### `chats`

List all chats with message counts.

```
chats
```

Output:

```
✦ Chat List — 2 chats
─────────────────────────────────────────
● general   12 messages
● dreams     4 messages
```

---

### `forget <chat-name>`

Delete a chat.

```
forget dreams
```

If you're inside the deleted chat, you move back to `.chat`.

---

### `rename <old-name> <new-name>`

Rename a chat and move into it.

```
rename dreams nightmare
rename general main
```

---

### `in <text>`

Ask the LLM a question.

```
in what is your name?
in explain Rust ownership in one sentence
```

**Requires:** `.model.llm` set to a `.gguf` model path.

```
set .model.llm "models/Qwen3-8B-Q4_K_M.gguf"
```

---

### `voice <text>`

Synthesize text into speech. Language auto-detected (English, Persian, ...).

```
voice hello world
voice سلام دنیا
```

---

## 10. Execution

### `apps`

List runnable programs under `.app`.

```
apps
```

---

### `<name>` or `.app.<name>`

Run a compiled plan at `.app.<name>`.

```
greet
.app.greet
```

---

### `<path>`

Run a plan at any AGFS path.

```
.tmp.plan
.my.deeply.nested.app
```

---

### `compile [-x] <source> [target]`

Compile an indented script into a JSON command tree.

```
compile .tmp.script
compile .tmp.script .tmp.plan
compile -x .tmp.script
```

See [§17 Compiler & Scripts](#17-compiler--scripts).

---

### `exec <command>`

Run a host OS command via `sh -c` (Unix) or `cmd /C` (Windows).

```
exec ls -la
exec echo hello
exec cat /etc/os-release
exec ps aux | grep ageno
```

---

### `asm <instructions>`

Assemble and execute machine code. `;` separates instructions.

```
asm mov eax, 42; ret
asm mov eax, 10; add eax, 32; ret
asm mov w0, #42; ret                  # ARM64
```

---

## 11. Programming — Control Flow

### `if <cond>: <body> [elif <cond>: <body>]... [else: <body>]`

Conditional branch. Inline (with `;`) or multi-line (indented).

**Inline:**
```
if $(x > 10): out "big" else: out "small"
if $status == active: out "active"
```

**Multi-line:**
```
if $(x > 10):
    out "big"
    out "tall"
elif $(x > 5):
    out "medium"
else:
    out "small"
```

**Conditions accept:**
- `$()` expression
- `$var` (bare or `${var}`)
- Numbers, strings (quoted), bools
- Bare words (treated as strings)

---

### `elif <cond>: <body>`

Else-if branch inside an `if` chain. Multi-line only makes sense when indented
at the same level as `if`.

```
if $x == 1: out "one" elif $x == 2: out "two"
```

---

### `else: <body>`

Default branch. Only valid inside `if`.

---

### `while <cond>: <body>`

Loop while condition is true.

```
var i 0
while $(i < 5):
    out $i
    var i $($i + 1)
```

**Features:**
- Up to 1,000,000 iterations (safety cap)
- Supports `break` and `continue`
- Condition re-evaluated each iteration

---

### `for <var> in <range|array> [step <n>]: <body>`

Python-like iteration.

**Range forms:**
```
for i in 0..5: out $i              # 0,1,2,3,4
for i in 0..10 step 2: out $i      # 0,2,4,6,8
for i in 10..0 step -1: out $i     # 10,9,...,1
for i in range(5): out $i          # 0,1,2,3,4
for i in range(3, 8): out $i       # 3,4,5,6,7
```

**Array iteration:**
```
var tags [a, b, c]
for t in $tags: out $t
for t in $tags step -1: out $t     # reverse
```

**With variables in range:**
```
var n 10
var s 2
for i in 0..$n step $s: out $i
for i in 0..$(n * 2) step $s: out $i
```

---

### `loop: <body>`

Infinite loop, must exit with `break`. 10,000,000 iteration cap.

```
var i 0
loop:
    out $i
    var i $($i + 1)
    if $(i >= 5): break
```

---

### `break`

Exit the innermost loop.

```
for i in 0..10:
    if $(i == 3): break
    out $i
```

---

### `continue`

Skip to next iteration.

```
for i in 0..10:
    if $(i % 2 == 0): continue
    out $i
```

---

### `match <value>:`

Multi-branch dispatch.

**Inline:**
```
match $x: 1: out "one"; 2: out "two"; _: out "other"
```

**Multi-line:**
```
match $status:
    active:  out "running"
    stopped: out "halted"
    _:       out "unknown"
```

**Rules:**
- Selector evaluated once
- First matching case executes
- `_` or `default:` is catch-all
- Comparison is type-strict: `"5"` ≠ `5`
- Case values can be numbers, quoted strings, bare words, `$var`, `$()`
- Lines indented at match level (not under a case) run **after** match

---

### `case <value>: <body>`

Explicit case inside `match`. Bare form (`1:`, `"a":`, `_:`) is preferred.

```
match $x:
    case 1: out "one"
    case 2: out "two"
    case _: out "other"
```

---

## 12. Programming — Functions

### `fun <name>(<params>): <body>`

Define a function. Also supports `fun <name>: <body>` (no params).

**Rules:**
- Name: letters, digits, underscore, not starting with a digit
- Not a reserved keyword or built-in
- Params: comma-separated identifiers
- Body: inline (with `;`) or indented

**Examples:**
```
fun add(a, b): ret $($a + $b)
fun pi: ret 3.14159
fun greet(name):
    out "hello, $name!"
```

**Calling — two equivalent forms:**

```
add(3, 4)         # paren form (python-like)
add 3 4           # space form (shell-like)
out $(add(3, 4))  # inline call, returns value
out $(add 3 4)
```

**$ret:** after any call, the result is in `$ret`.

```
add(3, 4)
out $ret          # 7
```

**Recursion:** supported up to 64 call depth.

```
fun factorial(n):
    if $(n <= 1): ret 1
    ret $(n * factorial($(n - 1)))
out $(factorial(5))    # 120
```

---

### `ret [value]`

Return from the current function.

```
fun double(x): ret $($x * 2)
fun early:
    ret "first"
    out "never"
```

**Notes:**
- No arg → returns Null
- `ret` also exits loops inside the function
- `ret` outside a function is ignored with a warning

---

## 13. Programming — Variables

### `var [name] [value]`

Define or list mutable runtime variables.

**List:**
```
var
```
Output:
```
  $x = 5      [var]
  $PI = 3.14  [val]
```

**Define:**
```
var x 5
var greeting "Hello world"
var arr [1, 2, 3]
var obj {"a": 1, "b": 2}
var expr $(2 + 3)
```

**Rules:**
- Session-only, not persisted to `.age`
- Reassignment allowed (unless the name is a `val`)
- Values: number, string (quoted or bare), bool, null, JSON array/object, `$()` expression

---

### `val [name] [value]`  ·  alias: `const`

Immutable constant. Can only be assigned once.

```
val PI 3.14
val GREETING "Hello world"
const MAX 100
```

Reassigning a `val` fails:
```
val x 5
var x 10   # Error: $x is a const
```

---

### `rev <name>[.key | [index] | ...]`

Remove a variable, or a key/index inside one.

```
rev greeting
rev arr.0
rev arr[2]
rev obj.name
rev nested.items[1].id
rev $greeting
```

---

### Reading Variables

Use `$name` or `${name}` anywhere in an argument:

```
out value: $x
set .agent.motto $greeting
if $status == active: out "yes"
```

**Type preservation:**
- `$x` alone → original type (string stays string, array stays array)
- `$x + 1` → string-joined (shell-like)
- `$(...)` → evaluated expression

**Array accessors:**
```
$arr.0
$arr[1]
$obj.name
$nested.a.0.b
```

---

## 14. Expression Evaluator

Use `$(...)` to evaluate an expression. Returns a `JsonValue`.

### Operators

| Operator | Description |
|---|---|
| `+` `-` `*` `/` `%` | Arithmetic |
| `^` | Power (right-associative) |
| `==` `!=` `<` `<=` `>` `>=` | Comparison |
| `&&` `\|\|` `!` | Logical |
| `-x` | Unary negation |
| `"a" + "b"` | String concatenation |
| `"ab" * 3` | String repetition |
| `3 * "hi"` | Same (commutative) |

**Precedence** (high → low): `^`, unary, `* / %`, `+ -`, comparison, `&&`, `||`

**Example:**
```
$(1 + 2 * 3)              # 7
$((1 + 2) * 3)            # 9
$(2 ^ 3 ^ 2)              # 512
$(-2 ^ 2)                 # -4
$(true + 1)               # 2
$(3 * "hi")               # hihihi
```

### Math Functions (unary)

| Function | Description |
|---|---|
| `sqrt(x)` | Square root |
| `cbrt(x)` | Cube root |
| `abs(x)` | Absolute value |
| `sign(x)` | -1, 0, or 1 |
| `sin/cos/tan(x)` | Trigonometry |
| `asin/acos/atan(x)` | Inverse trig |
| `sinh/cosh/tanh(x)` | Hyperbolic |
| `ln(x)` `log10(x)` `log2(x)` | Logarithms |
| `exp(x)` | e^x |
| `floor(x)` `ceil(x)` `round(x)` `trunc(x)` | Rounding |
| `deg(x)` `rad(x)` | Degree ↔ radian |

### Math Functions (binary / variadic)

| Function | Description |
|---|---|
| `atan2(y, x)` | Angle of (x,y) |
| `pow(a, b)` | a^b |
| `hypot(a, b)` | √(a² + b²) |
| `log(x)` / `log(x, base)` | Logarithm |
| `min(a, b, ...)` | Minimum |
| `max(a, b, ...)` | Maximum |

### String Functions

| Function | Description |
|---|---|
| `len(s)` | Character count |
| `upper(s)` `lower(s)` | Case conversion |
| `trim(s)` | Trim whitespace |
| `reverse(s)` | Reverse |
| `repeat(s, n)` | Repeat n times |
| `concat(a, b, ...)` | Concatenate |
| `substr(s, start, len)` | Substring (clamped) |
| `replace(s, find, sub)` | Replace |
| `contains(s, sub)` | Test containment |
| `starts_with(s, prefix)` | Test prefix |
| `ends_with(s, suffix)` | Test suffix |

### Type Functions

| Function | Description |
|---|---|
| `int(x)` | Truncate to integer |
| `float(x)` | Cast to float |
| `str(x)` | Convert to string |
| `bool(x)` | Convert to boolean |
| `type_of(x)` | "null" / "bool" / "number" / "string" / "array" / "object" |
| `is_num(x)` `is_str(x)` `is_bool(x)` `is_null(x)` | Type tests |

### Constants

| Constant | Value |
|---|---|
| `pi` / `PI` | 3.141592653589793 |
| `e` / `E` | 2.718281828459045 |
| `tau` / `TAU` | 6.283185307179586 |
| `true` `false` `null` `nil` | Literal values |

**Note:** Unknown identifiers are treated as **bare string literals** in comparisons.

```
$(hello == "hello")    # true
$(status == active)    # false unless $status is "active"
```

### Array Literals

```
$([1, 2, 3])
$(len([1, 2, 3]))      # 3
$(bool([]))            # false
$([[1,2], [3,4]])      # nested array
```

---

## 15. Cortex — Neural Network

A self-evolving text generator / Q&A system stored at `.cortex` in AGFS.

### `cortex init`

Create a fresh cortex with ~80-char ASCII seed, 1 hidden layer [16].

```
cortex init
```

---

### `cortex vocab <script...>`

Add Unicode script families to the vocabulary.

**Available scripts:**
```
latin, viet, cyrillic, greek, hebrew, arabic, syriac,
armenian, georgian, thaana, nko, tifinagh, ethiopic,
tibetan, devanagari, bengali, tamil, telugu, thai,
cjk, kana, hangul, cjk-all,
emoji, math, currency, punct, arrows, shapes, symbols,
programming, invisible,
runic, ogham, glagolitic, coptic, cuneiform, hieroglyphs,
braille, signwriting,
all-light (~3.5K chars), all (~50K chars — very slow)
```

```
cortex vocab ar ru emoji
cortex vocab all-light
```

---

### `cortex learn <text...>`

Feed training text. Appends to buffer and grows vocab from new characters.

```
cortex learn سلام دنیا hello world
```

---

### `cortex ingest <file> [epochs]`

Read a UTF-8 file (capped at 1 MB) and train immediately.

```
cortex ingest ~/corpus/mixed.txt 20
```

---

### `cortex train [epochs]`

Train on the accumulated buffer. Auto-grows if progress stalls.

```
cortex train 200
```

---

### `cortex autogrow <on|off>`

Toggle automatic hidden-layer growth (default: on).

```
cortex autogrow on
```

---

### `cortex grow [n]`

Manually add n neurons to the last hidden layer (default: 4).

```
cortex grow 8
```

---

### `cortex gen <seed> [len]`

Generate len chars following the seed (default: 48).

```
cortex gen a 64
cortex gen س 32
```

---

### `cortex ask <question>`

Ask a question — uses stored Q&A pairs for semantic retrieval.

```
cortex ask "What's your name"
```

---

### `cortex qa` — Manage Q&A pairs

```
cortex qa "question" "answer"     # add pair
cortex qa list                    # list all
cortex qa show "<q>"              # show details
cortex qa remove "<q>"            # delete
cortex qa clear                   # delete all
cortex qa auto on|off             # toggle auto-answer mode
```

---

### `cortex grammar <action> [lang]`

Manage grammar packs (built-in: `en`, `fa`, `ru`, ...).

```
cortex grammar en                  # install
cortex grammar fa
cortex grammar list                # available
cortex grammar active              # currently installed
cortex grammar remove en           # uninstall
```

---

### `cortex show`

Display architecture and training stats.

```
cortex show
```

---

### `cortex reset`

Wipe weights, embeddings, and training buffer. Vocab and config preserved.

```
cortex reset
```

---

## 16. Console

### `help [command]`

Show the full command guide or details for a specific command.

```
help
help create
help fun
?
```

---

### `info`

Show console and build info.

```
info
```

---

### `license`

Show the AGL v1.0 license.

```
license
```

---

### `clear`

Clear the console screen.

```
clear
```

---

### `out <markdown>`

Render markdown to colored terminal output.

```
out # Title
out **bold** and *italic* and `code`
out [link](https://ageno.ir)
```

**Supports:** headings, bold, italic, code, links, lists, quotes, tables.

---

### `shutdown`

Close the console. Auto-sleeps the awake agent before exit.

```
shutdown
```

---

## 17. Compiler & Scripts

### Writing a Script

A script is plain text with one command per line. Deeper indentation = nested
command.

```
# example: greet.script
out "Welcome"

if $user:
    out "hello, $user"
else:
    out "who are you?"

for i in 0..3:
    out "loop $i"
```

### `compile <source> [target]`

Read a script from AGFS, parse it into `{name, args, cmds}` nodes, save the
tree to a target path (or print it).

```
set .tmp.script "out hello\nout world"
compile .tmp.script                # print tree
compile .tmp.script .tmp.plan      # save to .tmp.plan
compile .tmp.script .app.greet     # save as runnable app
```

**Then run:**
```
greet
.app.greet
```

### `compile -x <source>`

Also execute the compiled tree immediately.

```
compile -x .tmp.script
```

### Syntax Rules

| Rule | Example |
|---|---|
| One command per line | `out hello` |
| First word = command name | `set name "Aida"` |
| Tab or 4-space indentation | `    out nested` |
| Comments start with `#` | `# this line is ignored` |
| Depth jumps allowed | 0 → 2 counts as direct child |
| Inline bodies use `;` | `if $x: out "a"; out "b"` |

### Compile to Runnable App

```
set .tmp.hello "out Hello, world!"
compile .tmp.hello .app.hello
hello                                # runs it
```

---

## 18. Error Handling

### Output Symbols

| Symbol | Meaning | Color |
|---|---|---|
| `✔` | Success | Green |
| `ℹ` | Info | Cyan |
| `!` | Warning | Yellow |
| `✖` | Error | Red |
| `tip:` | Hint (recovery) | Dim |
| `usage:` | Usage line | Dim |

### Runtime Errors vs Returns

- **Command errors** → `✖ <message>` + optional `tip:`
- **Expression errors** → propagated through `$()` with prefix `in $(...):`
- **Missing variable** → falls back to the literal `$name`

### Common Errors

| Error | Cause |
|---|---|
| `no agent is awake` | Run `wakeup <name> <password>` first |
| `unknown identifier` | Typo in constant, or missing `$` for variable |
| `undefined variable: $x` | Inside `$()` where variables are strict |
| `division by zero` | Math |
| `expected ':'` | Missing colon after `if`/`while`/`for` header |
| `execution depth exceeded` | Possible circular `fun` or `.app` plan |
| `while: missing body` | Block header without indented body |

---

## 19. Tips & Best Practices

### REPL Multi-line

Type a block header (`if`, `while`, `for`, `fun`, `match`, `loop`) — the
prompt changes to `...` until you enter an empty line or press Ctrl+C.

```
✦ if $x > 10:
  ...   out "big"
  ... 
```

### Inline Scripts

For one-liners, use `;`:

```
if $x: out "yes"; out "confirmed"
for i in 0..3: out $i; var sum $($sum + $i)
```

### Compile-First Workflow

For anything longer than 3–4 lines, write it as a `.app`:

```
set .tmp.script "..."
compile .tmp.script .app.<name>
<name>
```

### Variable Hygiene

- `var` for scratch values
- `val`/`const` for invariants
- `set` only for persistent AGFS state

### Debugging

```
list                    # what's around me
tree .agent             # whole subtree
show .agent.name        # one value
var                     # all runtime vars
```

### Backup Before Experiments

```
backup .cortex
cortex train 500
# if it breaks:
restore .cortex
```

### Function Call Forms

Both forms are equivalent — pick one per project for consistency:

```
myfn(1, 2)              # python-like
myfn 1 2                # shell-like
```

### Password Strength

All `.age` agents require strong passwords. Weak examples are rejected:

- ❌ `password123`
- ❌ `mani` (matches agent name)
- ❌ `aaaaaaaa` (repeats)
- ✅ `SecurE!42Pass`
- ✅ `MyAgent@2026`

---

**End of Documentation**

---

*ageno — Agent Control Console · (c) 2026 Mani Jamali · AGL v1.0*
