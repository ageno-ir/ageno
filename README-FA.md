
<pre>
╭────────────────────────────────────────────────────╮
│                                                    │
│                  ✦  A G E N O  ✦                   │
│                                                    │
│               Agent Control Console                │
│                                                    │
├────────────────────────────────────────────────────┤
│                   Version 0.0.1                    │
│               (c) 2026  Mani Jamali                │
╰────────────────────────────────────────────────────╯
</pre>

<h3 dir="rtl">🧠 یک محیط اجرایی برای ساخت، اجرا و تکامل عامل‌های هوش مصنوعی خودمختار.</h3>

[![Version](https://img.shields.io/badge/version-0.0.1-2563eb?style=for-the-badge&logo=semanticrelease&logoColor=white)](https://ageno.ir)
[![License](https://img.shields.io/badge/license-AGL%20v1.0-16a34a?style=for-the-badge&logo=opensourceinitiative&logoColor=white)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-6b7280?style=for-the-badge&logo=linux&logoColor=white)](https://ageno.ir)
[![Website](https://img.shields.io/badge/website-ageno.ir-9333ea?style=for-the-badge&logo=firefox&logoColor=white)](https://ageno.ir)
[![Made with ❤️](https://img.shields.io/badge/made%20with-%E2%9D%A4%EF%B8%8F-e11d48?style=for-the-badge)](https://ageno.ir)

</div>

---

<div align="center" dir="rtl">

**`ageno`** یک **زمان‌اجرای خودکفای عامل** است — هر عامل داده‌های رمزنگاری‌شده‌ی خود (AGFS) را در اختیار دارد،  
شبکه‌ی عصبی در حال تکامل خودش (Cortex) را اجرا می‌کند، و می‌تواند برنامه‌هایی را که با زبان اسکریپت داخلی ageno نوشته شده‌اند اجرا کند.

</div>

---

<a id="highlights"></a>

## ✨ ویژگی‌های برجسته

<table align="center" dir="ltr">
<tr>
<td align="center" width="33%">

### 🗂️ AGFS
وضعیت هر عامل یک **درخت JSON واحد** است که مانند یک پوسته (shell) آن را پیمایش می‌کنید.

</td>
<td align="center" width="33%">

### 🔐 رمزنگاری‌شده
شناسه‌های مشتق‌شده از **SHA3-512**، محافظت‌شده با رمز عبور در حالت سکون در فایل‌های `.age`.

</td>
<td align="center" width="33%">

### 🧠 کورتکس
یک **شبکه‌ی عصبی خودتکامل** برای تولید متن و پرسش‌وپاسخ.

</td>
</tr>
<tr>
<td align="center" width="33%">

### 🛠️ اسکریپت‌نویسی
جریان کنترل، توابع، متغیرها، و یک **ارزیاب کامل عبارت**.

</td>
<td align="center" width="33%">

### 📦 کامپایلر
اسکریپت‌ها به **درخت‌های دستور قابل حمل** کامپایل می‌شوند — آن‌ها را به‌عنوان اپ اجرا کنید.

</td>
<td align="center" width="33%">

### 💬 آماده‌ی LLM
یکپارچه‌سازی اختیاری **Qwen3** (یا سازگار) از طریق مدل‌های `.gguf`.

</td>
</tr>
<tr>
<td align="center" width="33%">

### 🧬 شبیه‌سازی
نمونه‌های اولیه‌ی عامل‌ها را به‌صورت `.egg` بسازید و به عامل‌های کامل `.age` تفریخ (hatch) کنید.

</td>
<td align="center" width="33%">

### 💾 پایداری
پشتیبان‌گیری، بازیابی، ذخیره و واردکردن وضعیت بین نصب‌ها.

</td>
<td align="center" width="33%">

### 🎙️ صدا
تبدیل متن به گفتار در چندین زبان — به‌طور خودکار تشخیص داده می‌شود.

</td>
</tr>
</table>

---

<a id="quick-start"></a>

## 🚀 شروع سریع

```bash
# 1. Launch the console (Linux/macOS)
chmod +x ageno-linux-x64
./ageno-linux-x64

# 2. Create your first agent
create mani Secret!42

# 3. Wake it up
wakeup mani Secret!42

# 4. Explore
whoami
show name
out "**Hello, world!**"
```

---

<a id="toc"></a>

## 📑 فهرست مطالب

1. [معرفی](#introduction)
2. [نصب و راه‌اندازی](#installation)
3. [مفاهیم اصلی](#core-concepts)
4. [دستورات — مرور کلی](#commands-overview)
5. [مدیریت عامل](#agent-management)
6. [پیمایش (AGFS)](#navigation)
7. [عملیات داده](#data-operations)
8. [پایداری](#persistence)
9. [گفت‌وگو و LLM](#chat-llm)
10. [اجرا](#execution)
11. [برنامه‌نویسی — جریان کنترل](#control-flow)
12. [برنامه‌نویسی — توابع](#functions)
13. [برنامه‌نویسی — متغیرها](#variables)
14. [ارزیاب عبارت](#expression-evaluator)
15. [کورتکس — شبکه‌ی عصبی](#cortex)
16. [کنسول](#console)
17. [کامپایلر و اسکریپت‌ها](#compiler)
18. [مدیریت خطا](#error-handling)
19. [نکات و بهترین شیوه‌ها](#tips)

---

<a id="introduction"></a>

## 🌱 معرفی

**ageno** یک کنسول کنترل عامل است — یک محیط اجرایی برای ساخت، اجرا و تکامل عامل‌های هوش مصنوعی خودمختار. هر عامل، یک موجودیت خودکفا و رمزنگاری‌شده است که داده‌های خودش (AGFS) را در اختیار دارد، شبکه‌ی عصبی خودش (کورتکس) را اجرا می‌کند، و می‌تواند برنامه‌هایی را که با زبان اسکریپت داخلی ageno نوشته شده‌اند اجرا کند.

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="installation"></a>

## 📦 نصب و راه‌اندازی

### دانلود و اجرا

| پلتفرم | دستور |
|---|---|
| **Windows x64** | `ageno-windows-x64.exe` |
| **Windows ARM-64** | `ageno-windows-arm64.exe` |
| **Linux x64** | `chmod +x ageno-linux-x64 && ./ageno-linux-x64` |
| **Linux ARM-64** | `chmod +x ageno-linux-arm64 && ./ageno-linux-arm64` |
| **macOS x64** | `chmod +x ageno-mac-x64 && ./ageno-mac-x64` |
| **macOS ARM-64** | `chmod +x ageno-mac-arm64 && ./ageno-mac-arm64` |

### بنر شروع

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

### خروج

```
shutdown
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="core-concepts"></a>

## 🧩 مفاهیم اصلی

### 🗂️ AGFS — فایل‌سیستم عامل

تمام داده‌های هر عامل در یک **درخت JSON واحد** زندگی می‌کند. با `go` آن را پیمایش کنید، با `show` / `list` / `tree` بازرسی کنید، و با `set`، `add`، `remove` و غیره آن را تغییر دهید.

```
.agent.name      → "Mani"
.agent.born      → 1787413200
.chat.dreams     → [ ... ]
.cortex          → { weights: [...], ... }
.app.greet       → [ { name: "out", args: [...] }, ... ]
```

**نحو مسیر (Path syntax):**

| شکل | معنی |
|---|---|
| `.agent` | مطلق (از ریشه) |
| `agent` | نسبی (از آدرس جاری) |
| `..` | والد |
| `.` | ریشه |
| `0` | اولین آیتم یک آرایه |
| `key.0.sub` | زنجیره |

### 🤖 عامل

یک فایل رمزنگاری‌شده‌ی `.age` شامل:

- `id` — هش SHA3-512 از `name + born + password`
- `name` — فقط حروف کوچک `a-z`
- `born` — مُهر زمانی یونیکس
- `gender` — به‌طور خودکار از نام تشخیص داده می‌شود
- `binary` — اطلاعات نسخه
- …به‌علاوه‌ی هر چیز دیگری در AGFS

### ⚖️ Runtime در برابر AGFS

| زمینه | ذخیره‌سازی | به `.age` پایدار می‌شود؟ |
|---|---|---|
| `var` / `val` | در حافظه به‌صورت `$name` | ❌ فقط جلسه |
| `set` / `object` / `array` | AGFS | ✅ |

### ⚙️ مدل مفسر

> [!NOTE]
> هر دستور یک گره است: `{ name, args, cmds }`. اسکریپت‌ها درخت‌های تو‌رفته‌ای از این گره‌ها هستند. اجرا به‌صورت عمق‌اول با محافظت در برابر چرخه است (حداکثر عمق: **۶۴**).

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="commands-overview"></a>

## 📜 دستورات — مرور کلی

| گروه | دستورات |
|---|---|
| 🧠 **کورتکس** | `cortex init/vocab/learn/ingest/train/grow/autogrow/gen/ask/qa/grammar/show/reset` |
| 🤖 **عامل** | `create`, `wakeup`, `sleep`, `die`, `clone`, `hatch`, `whoami` |
| 🧭 **پیمایش** | `go`, `show`, `list`, `tree` |
| 💾 **داده** | `set`, `edit`, `add`, `move`, `copy`, `remove`, `object`, `array` |
| 📀 **پایداری** | `backup`, `restore`, `save`, `import` |
| 💬 **گفت‌وگو و LLM** | `chat`, `chats`, `forget`, `rename`, `in`, `voice` |
| ⚡ **اجرا** | `apps`, `<name>`, `<path>`, `compile`, `exec`, `asm` |
| 🔀 **جریان کنترل** | `if`, `elif`, `else`, `while`, `for`, `loop`, `break`, `continue`, `match`, `case` |
| 🧮 **توابع** | `fun`, `ret` |
| 📊 **متغیرها** | `var`, `val` (نام مستعار `const`), `rev` |
| 🖥️ **کنسول** | `help`, `info`, `license`, `clear`, `out`, `shutdown` |

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="agent-management"></a>

## 🤖 مدیریت عامل

### `create <name> <password>`

یک عامل رمزنگاری‌شده‌ی `.age` جدید بسازید.

> [!IMPORTANT]
> **نام:** فقط حروف کوچک `a-z` — بدون رقم، نماد یا فاصله  
> **رمز عبور:** حداقل ۸ کاراکتر، باید شامل حروف بزرگ + کوچک + رقم + نماد باشد، بدون تکرار/توالی/نام عامل

```bash
create mani Secret!42
```

### `wakeup <name> <password>`

یک فایل `.age` را رمزگشایی کرده و در RAM بارگذاری کنید. بررسی می‌کند: فایل وجود دارد، `id` مطابقت دارد، رمز عبور رمزگشایی می‌شود.

```bash
wakeup mani 1382@1382Aa
```

### `sleep`

عامل جاری را به‌صورت `<name>.age` رمزگذاری کرده و از RAM خارج کنید.

```bash
sleep
```

### `die [-f]`

عامل بیدار را نابود کرده **و** فایل `.age` آن را حذف کنید. بدون `-f` تأیید می‌خواهد.

```bash
die           # asks "y/N"
die -f        # no confirmation
```

### `clone <name> <password>`

عامل جاری را در یک نمونه‌ی اولیه‌ی `<name>.egg` شبیه‌سازی کنید.

> [!TIP]
> یک `.egg` **بدون `id`** است، عامل اصلی را در `.agent.parent` جای‌گذاری می‌کند، و **تا زمانی که `hatch` نشود قابل اجرا نیست**.

```bash
clone aida NewSecret!42
```

### `hatch <name> <password>`

یک `.egg` را به یک عامل کامل `.age` با `id` و `born` تازه تبدیل کنید.

```bash
hatch aida NewSecret!42
```

### `whoami`

کارت شناسایی عامل جاری را نمایش دهید:

```
name / gender / id / born / address / password length / parent
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="navigation"></a>

## 🧭 پیمایش (AGFS)

### `go [path]`

به یک آدرس AGFS بروید. باید روی یک شیء یا آرایه فرود آیید.

```bash
go                      # root
go .agent               # absolute
go binary               # relative
go ..                   # parent
go ../..                # grandparent
go 0                    # first array item
```

### `show [path]`

یک مقدار **اولیه** (رشته، عدد، بولین، null) را نمایش دهید.

```bash
show
show name
show .agent.born
show active
```

### `list [path]`

کلیدهای یک شیء یا آیتم‌های یک آرایه را فهرست کنید.

```bash
list
list .agent
list .agent.tools
```

### `tree [path]`

نمای درختی بازگشتی از یک شیء یا آرایه.

```bash
tree
tree .agent
tree .agent.tags
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="data-operations"></a>

## 💾 عملیات داده

### `set <path> <value>`

یک مقدار **اولیه** در یک مسیر تنظیم کنید.

```bash
set name "Aida"
set age 25
set score 9.5
set active true
set nickname null
set .agent.color "#ff00aa"
```

> [!WARNING]
> اشیاء و آرایه‌ها **نمی‌توانند** با `set` ساخته شوند — از `object` / `array` استفاده کنید.

> [!NOTE]
> آرگومان‌های متعدد با فاصله به هم می‌پیوندند. رشته‌های نقل‌قول‌شده می‌توانند شامل فاصله باشند.

### `edit <path>`

یک ویرایشگر شبیه nano برای یک مقدار باز کنید.

| نوع موجود | حالت |
|---|---|
| رشته یا ناموجود | 📝 حالت متن |
| شیء / آرایه / عدد / بولین / null | 🔧 حالت JSON |

```bash
edit .agent.notes
edit .agent.config
```

> با `Ctrl+X` ذخیره کنید · با `Ctrl+X` روی محتوای تغییرنکرده، دور بریزید.

### `add <value>` · `add <array_path> <value>`

یک مقدار به یک آرایه اضافه کنید.

```bash
add hello                    # to current array
add 42
add tags hello               # to .tags array
add .agent.tags hello world  # multi-word value
add tags "hello world"
```

### `move <source> <destination>`

یک مقدار را در داخل AGFS جابه‌جا کنید.

```bash
move .agent.binary .agent.parent
move binary parent
move items.0 items.3
```

**قواعد:**
- مبدأ باید وجود داشته باشد؛ مقصد باید **وجود نداشته باشد**
- مقصد نمی‌تواند داخل مبدأ باشد
- مقصدهای آرایه‌ای فقط الحاقی هستند

### `copy <source> <destination>`

یک مقدار را در داخل AGFS کپی عمیق کنید.

```bash
copy .agent.binary .agent.binary-backup
copy binary backup
```

### `remove <path>`

هر مقداری را در مسیر حذف کنید (کلید شیء یا شاخص آرایه).

```bash
remove .agent.tags
remove name
remove items.0
```

> اگر آدرس جاری داخل زیردرخت حذف‌شده باشد، به عقب منتقل می‌شوید.

### `object <path>`

یک شیء خالی بسازید. والدهای گم‌شده به‌طور خودکار ساخته می‌شوند.

```bash
object tools
object .agent.tools
object a.b.c
```

### `array <path>`

یک آرایه‌ی خالی بسازید.

```bash
array tags
array .agent.tags
array items.0.tags
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="persistence"></a>

## 📀 پایداری

### `backup <path>`

یک عکس لحظه‌ای (snapshot) از `<path>` را در `<agent>-<hash>.age` رمزگذاری کنید. از **رمز عبور خودِ عامل** استفاده می‌کند — فقط این عامل می‌تواند بازیابی کند.

```bash
backup .agent.binary
backup binary
```

### `restore <path>`

یک مسیر را از پشتیبان خصوصی خودش بازیابی کنید. والدهای گم‌شده به‌طور خودکار ساخته می‌شوند.

```bash
restore .agent.binary
restore binary
```

### `save <path>`

با استفاده از یک کلید **مشترک** در `@<path>.age` ذخیره کنید. هر نصب ageno می‌تواند آن را وارد کند.

```bash
save .agent.binary
save binary
```

### `import <path>`

از یک فایل مشترک `@<path>.age` وارد کنید. نیازی به اعتبارنامه‌ی عامل نیست.

```bash
import .agent.binary
import binary
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="chat-llm"></a>

## 💬 گفت‌وگو و LLM

### `chat <chat-name>`

یک گفت‌وگو در `.chat.<name>` بسازید یا باز کنید و به آن وارد شوید.

> **قواعد:** بدون نقطه، حداقل یک حرف.

```bash
chat dreams
chat general
```

### `chats`

همه‌ی گفت‌وگوها را با تعداد پیام‌ها فهرست کنید.

```bash
chats
```

```text
✦ Chat List — 2 chats
─────────────────────────────────────────
● general   12 messages
● dreams     4 messages
```

### `forget <chat-name>`

یک گفت‌وگو را حذف کنید. اگر داخل گفت‌وگوی حذف‌شده باشید، به `.chat` برمی‌گردید.

```bash
forget dreams
```

### `rename <old-name> <new-name>`

یک گفت‌وگو را تغییر نام دهید و وارد آن شوید.

```bash
rename dreams nightmare
rename general main
```

### `in <text>`

از LLM یک سؤال بپرسید.

```bash
in what is your name?
in explain Rust ownership in one sentence
```

> [!IMPORTANT]
> **نیازمند:** تنظیم `.model.llm` به مسیر یک مدل `.gguf`.
>
> ```bash
> set .model.llm "models/Qwen3-8B-Q4_K_M.gguf"
> ```

### `voice <text>`

متن را به گفتار تبدیل کنید. زبان به‌طور خودکار تشخیص داده می‌شود (انگلیسی، فارسی، …).

```bash
voice hello world
voice سلام دنیا
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="execution"></a>

## ⚡ اجرا

### `apps`

برنامه‌های قابل اجرا زیر `.app` را فهرست کنید.

```bash
apps
```

### `<name>` · `.app.<name>`

یک پلن کامپایل‌شده در `.app.<name>` را اجرا کنید.

```bash
greet
.app.greet
```

### `<path>`

یک پلن در هر مسیری از AGFS را اجرا کنید.

```bash
.tmp.plan
.my.deeply.nested.app
```

### `compile [-x] <source> [target]`

یک اسکریپت تو‌رفته را به درخت دستور JSON کامپایل کنید.

```bash
compile .tmp.script
compile .tmp.script .tmp.plan
compile -x .tmp.script
```

> برای جزئیات به بخش [کامپایلر و اسکریپت‌ها](#compiler) مراجعه کنید.

### `exec <command>`

یک دستور سیستم‌عامل میزبان را از طریق `sh -c` (یونیکس) یا `cmd /C` (ویندوز) اجرا کنید.

```bash
exec ls -la
exec echo hello
exec cat /etc/os-release
exec ps aux | grep ageno
```

### `asm <instructions>`

کد ماشین را اسمبل و اجرا کنید. `;` دستورات را جدا می‌کند.

```bash
asm mov eax, 42; ret
asm mov eax, 10; add eax, 32; ret
asm mov w0, #42; ret                  # ARM64
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="control-flow"></a>

## 🔀 برنامه‌نویسی — جریان کنترل

### `if <cond>: <body> [elif <cond>: <body>]… [else: <body>]`

انشعاب شرطی. درون‌خطی (با `;`) یا چندخطی (تو‌رفته).

**درون‌خطی:**
```bash
if $(x > 10): out "big" else: out "small"
if $status == active: out "active"
```

**چندخطی:**
```bash
if $(x > 10):
    out "big"
    out "tall"
elif $(x > 5):
    out "medium"
else:
    out "small"
```

> **شرط‌ها می‌پذیرند:** عبارت `$()` · `$var` (خالی یا `${var}`) · اعداد، رشته‌ها، بولین‌ها · کلمات خالی (به‌عنوان رشته در نظر گرفته می‌شوند).

### `elif <cond>: <body>`

شاخه‌ی else-if در زنجیره‌ی `if`. چندخطی فقط زمانی معنا دارد که در همان سطح `if` تو‌رفته باشد.

```bash
if $x == 1: out "one" elif $x == 2: out "two"
```

### `else: <body>`

شاخه‌ی پیش‌فرض. فقط داخل `if` معتبر است.

### `while <cond>: <body>`

تا زمانی که شرط درست است حلقه بزنید.

```bash
var i 0
while $(i < 5):
    out $i
    var i $($i + 1)
```

> تا **۱٬۰۰۰٬۰۰۰** تکرار (سقف ایمنی) · پشتیبانی از `break` و `continue` · شرط در هر تکرار دوباره ارزیابی می‌شود.

### `for <var> in <range|array> [step <n>]: <body>`

تکرار شبیه پایتون.

**شکل‌های بازه:**
```bash
for i in 0..5: out $i              # 0,1,2,3,4
for i in 0..10 step 2: out $i      # 0,2,4,6,8
for i in 10..0 step -1: out $i     # 10,9,...,1
for i in range(5): out $i          # 0,1,2,3,4
for i in range(3, 8): out $i       # 3,4,5,6,7
```

**تکرار آرایه:**
```bash
var tags [a, b, c]
for t in $tags: out $t
for t in $tags step -1: out $t     # reverse
```

**با متغیر در بازه:**
```bash
var n 10
var s 2
for i in 0..$n step $s: out $i
for i in 0..$(n * 2) step $s: out $i
```

### `loop: <body>`

حلقه‌ی بی‌نهایت — باید با `break` خارج شود. سقف **۱۰٬۰۰۰٬۰۰۰** تکرار.

```bash
var i 0
loop:
    out $i
    var i $($i + 1)
    if $(i >= 5): break
```

### `break`

از درونی‌ترین حلقه خارج شوید.

```bash
for i in 0..10:
    if $(i == 3): break
    out $i
```

### `continue`

به تکرار بعدی بروید.

```bash
for i in 0..10:
    if $(i % 2 == 0): continue
    out $i
```

### `match <value>:`

ارسال چندشاخه‌ای.

**درون‌خطی:**
```bash
match $x: 1: out "one"; 2: out "two"; _: out "other"
```

**چندخطی:**
```bash
match $status:
    active:  out "running"
    stopped: out "halted"
    _:       out "unknown"
```

> [!TIP]
> - انتخاب‌گر **یک بار** ارزیابی می‌شود
> - اولین شاخه‌ی مطابق اجرا می‌شود
> - `_` یا `default:` همه‌گیر است
> - مقایسه **سخت‌گیرانه از نظر نوع** است: `"5"` ≠ `5`
> - مقادیر شاخه می‌توانند اعداد، رشته‌های نقل‌قول‌شده، کلمات خالی، `$var`، `$()` باشند
> - خطوط هم‌سطح match (نه زیر یک شاخه) **بعد از** match اجرا می‌شوند

### `case <value>: <body>`

شاخه‌ی صریح داخل `match`. شکل خالی (`1:`، `"a":`، `_:`) ترجیح داده می‌شود.

```bash
match $x:
    case 1: out "one"
    case 2: out "two"
    case _: out "other"
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="functions"></a>

## 🧮 برنامه‌نویسی — توابع

### `fun <name>(<params>): <body>`

یک تابع تعریف کنید. همچنین از `fun <name>: <body>` (بدون پارامتر) پشتیبانی می‌کند.

> **قواعد:** حروف/ارقام/زیرخط، نه شروع با رقم · نه کلمه‌ی کلیدی رزروشده و نه built-in · پارامترها شناسه‌های جدا‌شده با کاما · بدنه درون‌خطی (با `;`) یا تو‌رفته.

```bash
fun add(a, b): ret $($a + $b)
fun pi: ret 3.14159
fun greet(name):
    out "hello, $name!"
```

**فراخوانی — دو شکل معادل:**

```bash
add(3, 4)         # paren form   (python-like)
add 3 4           # space form   (shell-like)
out $(add(3, 4))  # inline call, returns value
out $(add 3 4)
```

**`$ret`** — پس از هر فراخوانی، نتیجه در `$ret` قرار دارد:

```bash
add(3, 4)
out $ret          # 7
```

**بازگشتی (Recursion)** تا عمق فراخوانی **۶۴** پشتیبانی می‌شود:

```bash
fun factorial(n):
    if $(n <= 1): ret 1
    ret $(n * factorial($(n - 1)))
out $(factorial(5))    # 120
```

### `ret [value]`

از تابع جاری بازگردید.

```bash
fun double(x): ret $($x * 2)
fun early:
    ret "first"
    out "never"
```

> بدون آرگومان → `Null` برمی‌گرداند · همچنین حلقه‌های داخل تابع را متوقف می‌کند · خارج از تابع با یک هشدار نادیده گرفته می‌شود.

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="variables"></a>

## 📊 برنامه‌نویسی — متغیرها

### `var [name] [value]`

متغیرهای قابل‌تغییر زمان اجرا را تعریف یا فهرست کنید.

**فهرست:**
```bash
var
```
```text
  $x = 5      [var]
  $PI = 3.14  [val]
```

**تعریف:**
```bash
var x 5
var greeting "Hello world"
var arr [1, 2, 3]
var obj {"a": 1, "b": 2}
var expr $(2 + 3)
```

> **قواعد:** فقط جلسه، به `.age` پایدار نمی‌شود · بازتخصیص مجاز است (مگر اینکه نام یک `val` باشد) · مقادیر: عدد، رشته (نقل‌قول‌شده یا خالی)، بولین، null، آرایه/شیء JSON، عبارت `$()`.

### `val [name] [value]` · نام مستعار: `const`

ثابت تغییرناپذیر. فقط یک بار می‌تواند مقداردهی شود.

```bash
val PI 3.14
val GREETING "Hello world"
const MAX 100
```

> [!WARNING]
> بازتخصیص یک `val` شکست می‌خورد:
> ```bash
> val x 5
> var x 10   # Error: $x is a const
> ```

### `rev <name>[.key | [index] | …]`

یک متغیر یا یک کلید/شاخص داخل آن را حذف کنید.

```bash
rev greeting
rev arr.0
rev arr[2]
rev obj.name
rev nested.items[1].id
rev $greeting
```

### 📖 خواندن متغیرها

از `$name` یا `${name}` در هر جایی از یک آرگومان استفاده کنید:

```bash
out value: $x
set .agent.motto $greeting
if $status == active: out "yes"
```

> [!NOTE]
> **حفظ نوع**
> - `$x` به‌تنهایی → نوع اصلی (رشته رشته می‌ماند، آرایه آرایه می‌ماند)
> - `$x + 1` → پیوند رشته‌ای (شبیه پوسته)
> - `$(...)` → عبارت ارزیابی‌شده

**دسترسی‌دهنده‌های آرایه:**
```bash
$arr.0
$arr[1]
$obj.name
$nested.a.0.b
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="expression-evaluator"></a>

## 🧠 ارزیاب عبارت

از `$(...)` برای ارزیابی یک عبارت استفاده کنید. یک `JsonValue` برمی‌گرداند.

### عملگرها

| عملگر | توضیح |
|---|---|
| `+` `-` `*` `/` `%` | حساب |
| `^` | توان (راست‌پیوند) |
| `==` `!=` `<` `<=` `>` `>=` | مقایسه |
| `&&` `\|\|` `!` | منطقی |
| `-x` | نقیض یکانی |
| `"a" + "b"` | پیوند رشته |
| `"ab" * 3` | تکرار رشته |
| `3 * "hi"` | همان (جابه‌جایی‌پذیر) |

> **اولویت** (بالا → پایین): `^` · یکانی · `* / %` · `+ -` · مقایسه · `&&` · `||`

```bash
$(1 + 2 * 3)              # 7
$((1 + 2) * 3)            # 9
$(2 ^ 3 ^ 2)              # 512
$(-2 ^ 2)                 # -4
$(true + 1)               # 2
$(3 * "hi")               # hihihi
```

### 🔢 توابع ریاضی — یکانی

| تابع | توضیح |
|---|---|
| `sqrt(x)` | ریشه‌ی دوم |
| `cbrt(x)` | ریشه‌ی سوم |
| `abs(x)` | قدر مطلق |
| `sign(x)` | -1، 0 یا 1 |
| `sin` `cos` `tan` | مثلثات |
| `asin` `acos` `atan` | مثلثات معکوس |
| `sinh` `cosh` `tanh` | هذلولی |
| `ln` `log10` `log2` | لگاریتم‌ها |
| `exp(x)` | e^x |
| `floor` `ceil` `round` `trunc` | گرد کردن |
| `deg(x)` `rad(x)` | درجه ↔ رادیان |

### 🔢 توابع ریاضی — دوتایی / چنده‌تایی

| تابع | توضیح |
|---|---|
| `atan2(y, x)` | زاویه‌ی (x, y) |
| `pow(a, b)` | a^b |
| `hypot(a, b)` | √(a² + b²) |
| `log(x)` / `log(x, base)` | لگاریتم |
| `min(a, b, …)` | کمینه |
| `max(a, b, …)` | بیشینه |

### 🔤 توابع رشته

| تابع | توضیح |
|---|---|
| `len(s)` | تعداد کاراکتر |
| `upper(s)` `lower(s)` | تبدیل حروف |
| `trim(s)` | حذف فضای خالی |
| `reverse(s)` | برعکس |
| `repeat(s, n)` | تکرار n بار |
| `concat(a, b, …)` | پیوند |
| `substr(s, start, len)` | زیررشته (محدودشده) |
| `replace(s, find, sub)` | جایگزینی |
| `contains(s, sub)` | آزمون شمول |
| `starts_with(s, prefix)` | آزمون پیشوند |
| `ends_with(s, suffix)` | آزمون پسوند |

### 🏷️ توابع نوع

| تابع | توضیح |
|---|---|
| `int(x)` | کوتاه کردن به عدد صحیح |
| `float(x)` | تبدیل به اعشاری |
| `str(x)` | تبدیل به رشته |
| `bool(x)` | تبدیل به بولین |
| `type_of(x)` | `"null"` / `"bool"` / `"number"` / `"string"` / `"array"` / `"object"` |
| `is_num` `is_str` `is_bool` `is_null` | آزمون نوع |

### 🔣 ثابت‌ها

| ثابت | مقدار |
|---|---|
| `pi` / `PI` | `3.141592653589793` |
| `e` / `E` | `2.718281828459045` |
| `tau` / `TAU` | `6.283185307179586` |
| `true` `false` `null` `nil` | مقادیر تحت‌اللفظی |

> [!NOTE]
> شناسه‌های ناشناخته در مقایسه‌ها به‌عنوان **رشته‌های خالی تحت‌اللفظی** در نظر گرفته می‌شوند.
>
> ```bash
> $(hello == "hello")    # true
> $(status == active)    # false unless $status is "active"
> ```

### 📚 آرایه‌های تحت‌اللفظی

```bash
$([1, 2, 3])
$(len([1, 2, 3]))      # 3
$(bool([]))            # false
$([[1,2], [3,4]])      # nested array
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="cortex"></a>

## 🕸️ کورتکس — شبکه‌ی عصبی

یک تولیدکننده‌ی متن / سیستم پرسش‌وپاسخ خودتکامل که در `.cortex` در AGFS ذخیره می‌شود.

### `cortex init`

یک کورتکس تازه با دانه‌ی ASCII حدود ۸۰ کاراکتری، ۱ لایه‌ی پنهان `[16]` بسازید.

```bash
cortex init
```

### `cortex vocab <script…>`

خانواده‌های اسکریپت یونیکد را به واژگان اضافه کنید.

**اسکریپت‌های موجود:**

```text
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

```bash
cortex vocab ar ru emoji
cortex vocab all-light
```

### `cortex learn <text…>`

متن آموزشی را تغذیه کنید. به بافر اضافه کرده و واژگان را از کاراکترهای جدید رشد می‌دهد.

```bash
cortex learn سلام دنیا hello world
```

### `cortex ingest <file> [epochs]`

یک فایل UTF-8 (محدود به **۱ مگابایت**) بخوانید و فوراً آموزش دهید.

```bash
cortex ingest ~/corpus/mixed.txt 20
```

### `cortex train [epochs]`

روی بافر انباشته آموزش دهید. در صورت توقف پیشرفت، به‌طور خودکار رشد می‌کند.

```bash
cortex train 200
```

### `cortex autogrow <on|off>`

رشد خودکار لایه‌ی پنهان را روشن/خاموش کنید (پیش‌فرض: `on`).

```bash
cortex autogrow on
```

### `cortex grow [n]`

به‌صورت دستی `n` نورون به آخرین لایه‌ی پنهان اضافه کنید (پیش‌فرض: **۴**).

```bash
cortex grow 8
```

### `cortex gen <seed> [len]`

`len` کاراکتر پس از دانه تولید کنید (پیش‌فرض: **۴۸**).

```bash
cortex gen a 64
cortex gen س 32
```

### `cortex ask <question>`

سؤال بپرسید — از جفت‌های Q&A ذخیره‌شده برای بازیابی معنایی استفاده می‌کند.

```bash
cortex ask "What's your name"
```

### `cortex qa` — مدیریت جفت‌های Q&A

```bash
cortex qa "question" "answer"     # add pair
cortex qa list                    # list all
cortex qa show "<q>"              # show details
cortex qa remove "<q>"            # delete
cortex qa clear                   # delete all
cortex qa auto on|off             # toggle auto-answer mode
```

### `cortex grammar <action> [lang]`

بسته‌های گرامر را مدیریت کنید (داخلی: `en`، `fa`، `ru`، …).

```bash
cortex grammar en                  # install
cortex grammar fa
cortex grammar list                # available
cortex grammar active              # currently installed
cortex grammar remove en           # uninstall
```

### `cortex show`

معماری و آمار آموزش را نمایش دهید.

```bash
cortex show
```

### `cortex reset`

وزن‌ها، جای‌گذاری‌ها و بافر آموزش را پاک کنید. واژگان و تنظیمات حفظ می‌شوند.

```bash
cortex reset
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="console"></a>

## 🖥️ کنسول

### `help [command]`

راهنمای کامل دستورات یا جزئیات یک دستور خاص را نمایش دهید.

```bash
help
help create
help fun
?
```

### `info`

اطلاعات کنسول و ساخت را نمایش دهید.

```bash
info
```

### `license`

مجوز AGL v1.0 را نمایش دهید.

```bash
license
```

### `clear`

صفحه‌ی کنسول را پاک کنید.

```bash
clear
```

### `out <markdown>`

مارک‌داون را به خروجی ترمینال رنگی تبدیل کنید.

```bash
out # Title
out **bold** and *italic* and `code`
out [link](https://ageno.ir)
```

> **پشتیبانی از:** سرفصل‌ها، پررنگ، ایتالیک، کد، لینک، لیست، نقل‌قول، جدول.

### `shutdown`

کنسول را ببندید. قبل از خروج، عامل بیدار را به‌طور خودکار به خواب می‌برد.

```bash
shutdown
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="compiler"></a>

## 🛠️ کامپایلر و اسکریپت‌ها

### ✍️ نوشتن یک اسکریپت

یک اسکریپت متن ساده است — یک دستور در هر خط. تو‌رفتگی بیشتر = دستور تودرتو.

```text
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

یک اسکریپت را از AGFS بخوانید، آن را به گره‌های `{name, args, cmds}` تجزیه کنید، درخت را در مسیر مقصد ذخیره کنید (یا چاپ کنید).

```bash
set .tmp.script "out hello\nout world"
compile .tmp.script                # print tree
compile .tmp.script .tmp.plan      # save to .tmp.plan
compile .tmp.script .app.greet     # save as runnable app
```

**سپس اجرا کنید:**

```bash
greet
.app.greet
```

### `compile -x <source>`

درخت کامپایل‌شده را بلافاصله اجرا هم بکنید.

```bash
compile -x .tmp.script
```

### 📐 قواعد نحو

| قاعده | مثال |
|---|---|
| یک دستور در هر خط | `out hello` |
| اولین کلمه = نام دستور | `set name "Aida"` |
| تو‌رفتگی با Tab یا ۴ فاصله | `    out nested` |
| کامنت‌ها با `#` شروع می‌شوند | `# this line is ignored` |
| پرش عمق مجاز است | `0 → 2` به‌عنوان فرزند مستقیم شمرده می‌شود |
| بدنه‌های درون‌خطی از `;` استفاده می‌کنند | `if $x: out "a"; out "b"` |

### 📦 کامپایل به اپ قابل اجرا

```bash
set .tmp.hello "out Hello, world!"
compile .tmp.hello .app.hello
hello                                # runs it
```

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="error-handling"></a>

## ⚠️ مدیریت خطا

### نمادهای خروجی

| نماد | معنی | رنگ |
|:---:|---|:---:|
| ✔ | موفقیت | 🟢 سبز |
| ℹ | اطلاعات | 🔵 فیروزه‌ای |
| ! | هشدار | 🟡 زرد |
| ✖ | خطا | 🔴 قرمز |
| `tip:` | راهنمایی (بازیابی) | ⚪ محو |
| `usage:` | خط استفاده | ⚪ محو |

### خطاهای زمان اجرا در برابر بازگشت‌ها

- **خطاهای دستور** → `✖ <message>` + `tip:` اختیاری
- **خطاهای عبارت** → از طریق `$()` با پیشوند `in $(...):` منتشر می‌شوند
- **متغیر گم‌شده** → به `$name` تحت‌اللفظی برمی‌گردد

### 🧯 خطاهای رایج

| خطا | علت |
|---|---|
| `no agent is awake` | ابتدا `wakeup <name> <password>` را اجرا کنید |
| `unknown identifier` | اشتباه تایپی در ثابت، یا `$` گم‌شده برای متغیر |
| `undefined variable: $x` | داخل `$()` جایی که متغیرها سخت‌گیرانه‌اند |
| `division by zero` | ریاضی |
| `expected ':'` | کولون گم‌شده بعد از سرآیند `if` / `while` / `for` |
| `execution depth exceeded` | `fun` یا پلن `.app` دایره‌ای احتمالی |
| `while: missing body` | سرآیند بلوک بدون بدنه‌ی تو‌رفته |

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<a id="tips"></a>

## 💡 نکات و بهترین شیوه‌ها

### ⌨️ REPL چندخطی

یک سرآیند بلوک تایپ کنید (`if`، `while`، `for`، `fun`، `match`، `loop`) — اعلان (prompt) به `...` تغییر می‌کند تا خط خالی وارد کنید یا `Ctrl+C` بزنید.

```text
✦ if $x > 10:
  ...   out "big"
  ...
```

### ⚡ اسکریپت‌های درون‌خطی

برای یک‌خطی‌ها از `;` استفاده کنید:

```bash
if $x: out "yes"; out "confirmed"
for i in 0..3: out $i; var sum $($sum + $i)
```

### 📦 جریان کاری «اول کامپایل»

برای هر چیزی بیش از ۳ تا ۴ خط، آن را به‌صورت یک `.app` بنویسید:

```bash
set .tmp.script "..."
compile .tmp.script .app.<name>
<name>
```

### 🧹 بهداشت متغیرها

| استفاده | برای |
|---|---|
| `var` | مقادیر موقت |
| `val` / `const` | ثابت‌ها |
| `set` | وضعیت پایدار AGFS |

### 🐞 اشکال‌زدایی

```bash
list                    # what's around me
tree .agent             # whole subtree
show .agent.name        # one value
var                     # all runtime vars
```

### 💾 قبل از آزمایش‌ها پشتیبان بگیرید

```bash
backup .cortex
cortex train 500
# if it breaks:
restore .cortex
```

### 🧮 شکل‌های فراخوانی تابع

هر دو شکل معادل‌اند — برای هر پروژه یکی را انتخاب کنید:

```bash
myfn(1, 2)              # python-like
myfn 1 2                # shell-like
```

### 🔐 قدرت رمز عبور

تمام عامل‌های `.age` به رمز عبور **قوی** نیاز دارند:

| ❌ ضعیف | ✅ قوی |
|---|---|
| `password123` | `SecurE!42Pass` |
| `mani` *(منطبق با نام عامل)* | `MyAgent@2026` |
| `aaaaaaaa` *(تکرار)* | |

<div align="left" dir="rtl"><sub><a href="#toc">⬆ بازگشت به بالا</a></sub></div>

---

<div align="center" dir="rtl">

### ✦ ageno — کنسول کنترل عامل ✦

**© ۲۰۲۶ مانی جمالی · تحت مجوز [AGL v1.0](LICENSE)**

[![Website](https://img.shields.io/badge/ageno.ir-visit-9333ea?style=flat-square&logo=firefox&logoColor=white)](https://ageno.ir)
[![Made with ❤️](https://img.shields.io/badge/made%20with-%E2%9D%A4%EF%B8%8F-e11d48?style=flat-square)](https://ageno.ir)

</div>
