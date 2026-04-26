<!--
████████████████████████████████████████████████████████████████████████████████████
█                                                                                  █
█                              N O V I R L I N K                                  █
█                    Complete Platform Documentation — التوثيق الكامل             █
█                                                                                  █
█                              novirlink.shop                                      █
█                                                                                  █
████████████████████████████████████████████████████████████████████████████████████

   Version: 1.0  |  Stack: Node.js + Discord.js v14 + SQLite  |  Host: AWS Lightsail
   Last Updated: 2026
-->

<div align="center">

<img src="https://novirlink.shop/favicon.png" width="120" alt="NovirLink" />

# NovirLink

**منصة ربط Discord × VRChat الاحترافية**  
*The Professional Discord × VRChat Bridge Platform*

[![Platform](https://img.shields.io/badge/🌐_Website-novirlink.shop-b47aff?style=for-the-badge)](https://novirlink.shop)
[![Discord](https://img.shields.io/badge/Discord-Bot-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://novirlink.shop)
[![VRChat](https://img.shields.io/badge/VRChat-Integration-00B4FF?style=for-the-badge)](https://novirlink.shop)

---

**اختر لغتك — Choose your language:**

**[🇸🇦 العربية](#-بالعربي)** &nbsp;|&nbsp; **[🇺🇸 English](#-english)**

</div>

---

<br/>
<br/>

# 🇸🇦 بالعربي

## ما هي NovirLink؟

**NovirLink** منصة متكاملة تربط سيرفرات Discord بمجموعات VRChat.  
تُتيح لأصحاب السيرفرات إدارة **Allowlist** و**الحظر** و**الاستئناف** من مكان واحد — عبر بوت Discord ولوحة تحكم ويب.

> 🔗 الموقع الرسمي: **[novirlink.shop](https://novirlink.shop)**

---

## كيف تعمل المنصة؟

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   Discord Member                                           │
│        │                                                    │
│        │  /link vrchat_name                                 │
│        ▼                                                    │
│   ┌─────────────┐   verify name   ┌─────────────────┐      │
│   │  NovirLink  │ ──────────────► │   VRChat API    │      │
│   │    Bot      │ ◄────────────── │                 │      │
│   └──────┬──────┘   name found    └─────────────────┘      │
│          │                                                  │
│          │ save                                             │
│          ▼                                                  │
│   ┌─────────────┐                 ┌─────────────────┐      │
│   │  Database   │                 │  Web Dashboard  │      │
│   │  (SQLite)   │ ◄─────────────► │ novirlink.shop  │      │
│   └─────────────┘                 └─────────────────┘      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### الخطوات بالتفصيل:

| # | الخطوة | التفاصيل |
|---|--------|----------|
| 1 | العضو يكتب `/link اسمه` | من داخل سيرفر Discord |
| 2 | البوت يبحث في VRChat API | للتحقق من وجود الاسم |
| 3 | الاسم يُحفظ في قاعدة البيانات | مرتبط بـ Discord ID |
| 4 | العضو يُضاف للـ Allowlist | في المجموعة أو الخريطة |
| 5 | عند فقدان الرول | يُحذف تلقائياً من القائمة |

---

## الأنظمة الرئيسية

### 🔗 نظام الربط — Allowlist
يسمح لأعضاء Discord بربط اسم VRChat الخاص بهم ليكونوا ضمن قائمة المسموح لهم.

- ✅ التحقق من الاسم عبر VRChat API قبل الحفظ
- ✅ دعم حتى **3 أدوار** مختلفة لكل سيرفر
- ✅ مزامنة تلقائية كل 10 دقائق
- ✅ ملف تعريف عالمي — اسمك يظهر في كل السيرفرات

```
Discord Role ✓  →  /link VRChat_Name  →  Added to Allowlist ✓
Discord Role ✗  →  Auto-removed from Allowlist after sync
```

---

### 🚫 نظام الحظر — Ban System
حظر اللاعبين من VRChat Group مباشرةً من Discord.

- ✅ حظر فوري في VRChat من خلال أمر واحد
- ✅ مدد الحظر: **1 ساعة ← 1 يوم ← 1 أسبوع ← 1 شهر ← دائم**
- ✅ رفع الحظر تلقائي عند انتهاء المدة
- ✅ سجل كامل بكل الحظرات والأسباب

```
/ban PlayerName 7d "سبب الحظر"
     │
     ├──► VRChat API: banned from group ✓
     ├──► Database: saved with expiry timer
     └──► After 7 days: auto-unban ✓
```

---

### ⚖️ نظام الاستئناف — Appeals
نظام متكامل يتيح للمحظورين تقديم طلب استئناف.

```
المستخدم المحظور                    صاحب السيرفر
       │                                  │
       ▼                                  ▼
 appeal.html              appeals-review.html?guildId=ID
       │                                  │
       │  يرى سبب حظره                    │  يراجع الطلبات
       │  يكتب سبب الاستئناف              │  يقبل أو يرفض
       │                                  │
       └──────────► Database ◄────────────┘
                        │
              إذا قُبل: VRChat Auto-Unban ✓
```

- ✅ المحظور يرى سبب حظره تلقائياً عند تقديم الطلب
- ✅ صفحة مراجعة مستقلة لكل سيرفر
- ✅ القبول يرفع الحظر تلقائياً من VRChat
- ✅ تتبع حالة الطلب من نفس الصفحة

---

### 📊 لوحة التحكم — Dashboard
واجهة ويب كاملة على [novirlink.shop](https://novirlink.shop)

| القسم | ما يتيحه |
|-------|---------|
| **الأعضاء** | عرض المرتبطين، بحث، حذف |
| **الحظر** | إضافة، رفع، عرض القائمة |
| **الأدمنز** | إضافة وإزالة صلاحيات |
| **السجلات** | كل الأحداث مرتبة بالتاريخ |
| **الإحصائيات** | رسوم بيانية وأرقام |
| **الإعدادات** | الرول، القناة، المجموعة |
| **الاستئنافات** | مراجعة طلبات الحظر |

---

## أوامر البوت

### 👤 للأعضاء
| الأمر | الوصف |
|-------|-------|
| `/link <vrchat_name>` | ربط اسم VRChat الخاص بك |

### ⚙️ للأدمنز
| الأمر | الوصف |
|-------|-------|
| `/setup enable` | تفعيل النظام في السيرفر |
| `/setup role <role>` | تحديد الرول المطلوب |
| `/setup group <id>` | ربط مجموعة VRChat |
| `/setup channel <channel>` | قناة الإشعارات |
| `/setup info` | معلومات الإعداد الحالي |
| `/unlink <user>` | إزالة ربط عضو |
| `/ban <name> <duration> <reason>` | حظر لاعب |
| `/unban <name>` | رفع حظر لاعب |
| `/banlist` | قائمة المحظورين |
| `/blacklist add/remove/list` | القائمة السوداء |
| `/admin add/remove/list` | إدارة الأدمنز |
| `/stats` | إحصائيات السيرفر |


---

## صفحات الموقع

| الصفحة | الرابط | لمن؟ |
|--------|--------|------|
| لوحة التحكم | `novirlink.shop` | أصحاب السيرفرات |
| تقديم استئناف | `novirlink.shop/appeal.html` | المستخدمون المحظورون |
| مراجعة الاستئنافات | `novirlink.shop/appeals-review.html?guildId=ID` | أصحاب السيرفرات |

---

## 🔗 كيفية ربط مجموعة VRChat

لتفعيل نظام الحظر والـ Allowlist، يجب ربط مجموعة VRChat بالسيرفر.

### الخطوات:

1. في مجموعتك على VRChat، أضف حساب البوت **`novir studio`** وامنحه دور **Moderator**، أو فعّل صلاحية **Ban Members** يدوياً
2. انسخ ID المجموعة من رابطها:  
   `https://vrchat.com/home/group/grp_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
3. في سيرفر Discord، نفّذ الأمر:  
   `/setup group grp_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
4. البوت يتحقق تلقائياً من الصلاحيات ويعرض رسالة تأكيد
5. بعد التأكيد ✅ — تبدأ أوامر `/ban` و `/unban` بالعمل مباشرةً في VRChat

> **ملاحظة:** إذا ظهر خطأ "لا يمكن ربط القروب"، تأكد أولاً من منح البوت صلاحية **Ban Members** في VRChat ثم أعد تنفيذ الأمر.

---

## 🎮 الاتصال بالمنصة من خلال Udon

يمكن ربط خريطة VRChat مباشرةً بالمنصة لجلب قائمة المسموح لهم، صور اللاعبين، ورسائل مخصصة.

---

### ℹ️ مقدمة

**Udon** هو نظام البرمجة المدمج في VRChat SDK. يستخدم **`VRCUrl`** لطلب بيانات من مواقع خارجية عبر **String Downloader** أو **Image Downloader**.

المنصة توفر **نقاط اتصال** جاهزة:

| النقطة | الرابط | ما ترجعه |
|--------|--------|----------|
| **Allowlist** | `/world/WORLD_KEY/allowlist.json` | قائمة الأسماء المربوطة |
| **كل الصور** | `/world/WORLD_KEY/images.json` | قائمة JSON بكل الصور |
| **صور Landscape** | `/world/WORLD_KEY/images-landscape.json` | صور أفقية فقط |
| **صور Portrait** | `/world/WORLD_KEY/images-portrait.json` | صور عمودية فقط |
| **الصورة الحالية** | `/world/WORLD_KEY/current-image/landscape` | ملف الصورة مباشرة (binary) |

> للحصول على `WORLD_KEY` الخاص بسيرفرك: افتح لوحة التحكم على [novirlink.shop](https://novirlink.shop) ← الإعدادات.

---

### 📌 جلب Allowlist (String Downloader)

يستخدم هذا لتحميل قائمة المسموح لهم واستخدامها للتحقق من صلاحية المستخدم عند دخول الخريطة.

**الأدوات المطلوبة في الخريطة:**

| المكون | النوع | وظيفته |
|---------|------|----------|
| `VRC String Downloader` | Component | يجلب البيانات كنص |
| `UdonBehaviour` | Component | يعالج البيانات بعد الجلب |
| `VRCUrl` | Variable | يخزن رابط المنصة |

**الخطوات:**

1. أضف مكون `VRC String Downloader` لنفس الكائن
2. في متغير الـ URL ضع رابط المنصة:
   ```
   https://novirlink.shop/world/WORLD_KEY/allowlist.json
   ```
3. في سكريبت Udon استخدم `DownloadString(url)` لبدء التحميل
4. في دالة `OnStringLoadSuccess` تصلك البيانات كنص JSON
5. حلّل النص وابحث عن اسم اللاعب ضمن مصفوفة `allowList`
6. إذا وُجد الاسم → سمح له بالدخول أو فعّل الميزات / إذا لم يُوجد → طرده أو لا تفعل شيئاً

**شكل البيانات العائدة (JSON):**
```json
{
  "allowList": ["PlayerName1", "PlayerName2", "PlayerName3"],
  "updatedAt": "2026-04-26T12:00:00Z",
  "playerCount": 42
}
```

> **ملاحظة مهمة:** يجب إضافة دومين `novirlink.shop` في قائمة الـ **Allowlisted URLs** في إعدادات مشروع VRChat (خانة String Downloader URLs).

---

### 🖼️ عرض صور الغاليري (Image Downloader)

يمكنك رفع صور من الداشبورد (لافتات، إعلانات، صور ترحيب) وعرضها في خريطتك تلقائياً دون الحاجة لإعادة بناء العالم.

**أولاً: رفع الصور من الداشبورد**

1. افتح [novirlink.shop](https://novirlink.shop) وسجّل دخولك
2. اختر سيرفرك → تبويب **Gallery / الصور**
3. الصق رابط الصورة (من Imgur أو Discord أو أي CDN) واضغط **إضافة**
4. اختر نوع الصورة: **Landscape (أفقية)** أو **Portrait (عمودية)**
5. يمكنك ترتيبها أو تفعيل/تعطيل كل صورة بشكل مستقل

---

**ثانياً: جلب الصورة في Udon**

الطريقة الأسهل — تحميل الصورة الحالية مباشرةً كـ binary:

| المكون | النوع | وظيفته |
|---------|------|----------|
| `VRC Image Downloader` | Component | يجلب الصورة كـ Texture2D |
| `RawImage` / `MeshRenderer` | Component | يعرض الصورة على سطح في الخريطة |
| `TextureInfo` | Object | إعدادات الصورة |

**الخطوات:**

1. في متغير الـ URL ضع رابط الصورة الحالية:
   ```
   https://novirlink.shop/world/WORLD_KEY/current-image/landscape
   ```
   أو للصورة العمودية:
   ```
   https://novirlink.shop/world/WORLD_KEY/current-image/portrait
   ```
2. في سكريبت Udon استخدم `DownloadImage(url, textureInfo)` لبدء التحميل
3. في دالة `OnImageLoadSuccess` طبق الـ Texture على `RawImage` أو `Renderer.material`
4. في `OnImageLoadError` اعرض صورة افتراضية (placeholder)
5. الصورة تتحدث تلقائياً كلما تغيّرت في الداشبورد

---

**الطريقة المتقدمة — جلب قائمة كل الصور (للتبديل بينها):**

1. استخدم `VRC String Downloader` لجلب:
   ```
   https://novirlink.shop/world/WORLD_KEY/images-landscape.json
   ```
2. ستصلك بيانات JSON:
   ```json
   {
     "worldKey": "abcdef1234567890",
     "orientation": "landscape",
     "imageCount": 3,
     "images": [
       { "url": "https://...", "label": "Welcome Banner" },
       { "url": "https://...", "label": "Event Poster" }
     ]
   }
   ```
3. في Udon حلّل JSON واستخدم `DownloadImage(url)` لكل صورة
4. ضع الصور في مصفوفة وبدّل بينها بـ timer أو زر

> **ملاحظة مهمة:** يجب إضافة دومين `novirlink.shop` لقائمة **Image Downloader URLs** في إعدادات مشروع VRChat.

---

### 💬 عرض رسائل المنصة (String Downloader)

يمكنك كتابة رسائل من الداشبورد (إعلانات، قواعد، ترحيب) وتظهر في الخريطة تلقائياً دون إعادة بناء المشروع.

**أولاً: إضافة الرسائل من الداشبورد**

1. افتح [novirlink.shop](https://novirlink.shop) وسجّل دخولك
2. اختر سيرفرك ← تبويب **Messages / الرسائل**
3. عندك **خانتان (Slot 1 و Slot 2)** — كل خانة تدعم عدة رسائل
4. لكل رسالة اكتب النص (`text`) وحدد مدة العرض (`duration`) بالثواني
5. الرسائل تتحدث فوراً بمجرد حفظها — دون لمس المشروع

---

**ثانياً: جلب الرسائل في Udon**

1. استخدم `VRC String Downloader` لجلب:
   ```
   https://novirlink.shop/world/WORLD_KEY/messages-1.json
   ```
   أو للخانة الثانية:
   ```
   https://novirlink.shop/world/WORLD_KEY/messages-2.json
   ```
2. شكل البيانات العائدة (JSON):
   ```json
   {
     "slot": 1,
     "messageCount": 2,
     "messages": [
       { "text": "مرحبا في العالم!", "duration": 5 },
       { "text": "تمتع بزيارتك 🎉", "duration": 4 }
     ]
   }
   ```
3. في Udon حلّل JSON وكرر على المصفوفة
4. اعرض كل رسالة في `TextMeshPro` واستخدم `duration` كمدة ظهورها (بالثواني)
5. كرر الحلقة أو شغّلها عند `OnPlayerJoined`

---

### ⚠️ اشتراطات Udon المهمة

| المتطلب | التفاصيل |
|---------|----------|
| **SDK** | VRChat SDK 3.x (نظام Udon) |
| **إضافة URL** | يجب إضافة `novirlink.shop` لـ String + Image Downloader Allowlists |
| **التحديث** | البيانات حية — لا حاجة لتخزين محلي |
| **المعدل** | الطلبات حسب قواعد VRChat — لا تطلب بكثرة |
| **الخصوصية** | البيانات عامة — لا تضع معلومات حساسة فيها |

---

## 🔒 الخصوصية وأمان البيانات

**خصوصيتك أولويتنا.**

- ✅ جميع البيانات المخزنة (الأسماء، الحظرات، الروابط) **خاصة بك** وبسيرفرك فقط
- ✅ **لا نستخدم بياناتك** لأي غرض خارجي — لا تحليلات، لا مبيعات، لا مشاركة مع أطراف ثالثة
- ✅ كل سيرفر معزول عن الآخر — مديرو سيرفر لا يرون بيانات سيرفر آخر
- ✅ **WORLD_KEY** الخاص بك سري — لا تشاركه مع أشخاص غير موثوقين
- ✅ يمكنك حذف جميع بياناتك في أي وقت من الداشبورد
- ⚠️ البيانات العامة (Allowlist, رسائل, صور) مرئية لأي شخص يملك الـ WORLD_KEY — لا تضع فيها معلومات حساسة

---

## ⚖️ مقارنة NovirLink مع المنصات الأخرى

| الميزة | **NovirLink** | DisBridge | VRCX |
|--------|:-------------:|:---------:|:----:|
| مزامنة رول Discord مع صلاحيات العالم | ✅ | ✅ | ❌ |
| Whitelist (قائمة مسموح لهم) من Discord | ✅ | ✅ | ❌ |
| حظر/رفع حظر في VRChat من Discord | ✅ | ❌ | ❌ |
| نظام استئناف الحظر | ✅ | ❌ | ❌ |
| لوحة تحكم ويب | ✅ | ❌ | ❌ |
| تحميل صور للخريطة | ✅ | ❌ | ❌ |
| رسائل مخصصة للخريطة | ✅ | ❌ | ❌ |
| Keypad / RoleTags / RoleBoard | ❌ | ✅ | ❌ |
| تكامل Udon (VRChat worlds) | ✅ | ✅ | ❌ |
| تطبيق سطح مكتب | ❌ | ❌ | ✅ |
| السعر | 💰 **$13/شهر** | 💰 **$25+** | مجاني |

> **DisBridge**: أداة Udon تربط رولات Discord بصلاحيات العالم (أبواب، VIP، toggles) — لا يوجد لديها نظام بان، استئناف، أو لوحة ويب. أرخص خطة بـ $25.  
> **VRCX**: تطبيق سطح مكتب لتتبع الأصدقاء والعوالم — لا يتصل بـ Discord ولا يدير بانات.

---
---

<br/>
<br/>

# 🇺🇸 English

## What is NovirLink?

**NovirLink** is a complete platform that bridges Discord servers with VRChat groups.  
It allows server owners to manage their **Allowlist**, **bans**, and **appeals** from one place — through a Discord bot and a web dashboard.

> 🔗 Official Website: **[novirlink.shop](https://novirlink.shop)**

---

## How Does It Work?

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   Discord Member                                           │
│        │                                                    │
│        │  /link vrchat_name                                 │
│        ▼                                                    │
│   ┌─────────────┐   verify name   ┌─────────────────┐      │
│   │  NovirLink  │ ──────────────► │   VRChat API    │      │
│   │    Bot      │ ◄────────────── │                 │      │
│   └──────┬──────┘   name found    └─────────────────┘      │
│          │                                                  │
│          │ save                                             │
│          ▼                                                  │
│   ┌─────────────┐                 ┌─────────────────┐      │
│   │  Database   │                 │  Web Dashboard  │      │
│   │  (SQLite)   │ ◄─────────────► │ novirlink.shop  │      │
│   └─────────────┘                 └─────────────────┘      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Step-by-step:

| # | Step | Details |
|---|------|---------|
| 1 | Member types `/link their_name` | Inside a Discord server |
| 2 | Bot searches VRChat API | To verify the name exists |
| 3 | Name saved to database | Linked to Discord ID |
| 4 | Member added to Allowlist | In the group or world |
| 5 | If role is lost | Auto-removed from the list |

---

## Core Systems

### 🔗 Link System — Allowlist
Allows Discord members to link their VRChat name to be part of the allowed list.

- ✅ Validates name via VRChat API before saving
- ✅ Supports up to **3 different roles** per server
- ✅ Auto-sync every 10 minutes
- ✅ Global profile — your name appears across all servers

```
Discord Role ✓  →  /link VRChat_Name  →  Added to Allowlist ✓
Discord Role ✗  →  Auto-removed from Allowlist after sync
```

---

### 🚫 Ban System
Ban players from a VRChat Group directly from Discord.

- ✅ Instant ban in VRChat from a single command
- ✅ Durations: **1 hour ← 1 day ← 1 week ← 1 month ← permanent**
- ✅ Auto-unban when duration expires
- ✅ Full ban log with reasons and timestamps

```
/ban PlayerName 7d "ban reason"
     │
     ├──► VRChat API: banned from group ✓
     ├──► Database: saved with expiry timer
     └──► After 7 days: auto-unban ✓
```

---

### ⚖️ Appeals System
A complete system that allows banned users to submit an appeal.

```
Banned User                          Server Owner
     │                                    │
     ▼                                    ▼
appeal.html                 appeals-review.html?guildId=ID
     │                                    │
     │  Sees their ban reason             │  Reviews requests
     │  Writes appeal reason             │  Approves or rejects
     │                                    │
     └──────────► Database ◄─────────────┘
                      │
           If approved: VRChat Auto-Unban ✓
```

- ✅ Banned user sees their ban reason automatically when submitting
- ✅ Separate review page per server
- ✅ Approval triggers automatic VRChat unban
- ✅ Track appeal status from the same page

---

### 📊 Dashboard
Full web interface at [novirlink.shop](https://novirlink.shop)

| Section | What it provides |
|---------|-----------------|
| **Members** | View linked accounts, search, delete |
| **Bans** | Add, remove, view ban list |
| **Admins** | Add and remove admin permissions |
| **Logs** | All events sorted by date |
| **Statistics** | Charts and numbers |
| **Settings** | Role, channel, group |
| **Appeals** | Review ban appeal requests |

---

## Bot Commands

### 👤 For Members
| Command | Description |
|---------|-------------|
| `/link <vrchat_name>` | Link your VRChat name |

### ⚙️ For Admins
| Command | Description |
|---------|-------------|
| `/setup enable` | Activate the system in your server |
| `/setup role <role>` | Set the required role |
| `/setup group <id>` | Link a VRChat group |
| `/setup channel <channel>` | Set notification channel |
| `/setup info` | View current setup info |
| `/unlink <user>` | Remove a member's link |
| `/ban <name> <duration> <reason>` | Ban a player |
| `/unban <name>` | Unban a player |
| `/banlist` | View ban list |
| `/blacklist add/remove/list` | Blacklist management |
| `/admin add/remove/list` | Admin management |
| `/stats` | Server statistics |


---

## Website Pages

| Page | URL | For |
|------|-----|-----|
| Dashboard | `novirlink.shop` | Server owners |
| Submit appeal | `novirlink.shop/appeal.html` | Banned users |
| Review appeals | `novirlink.shop/appeals-review.html?guildId=ID` | Server owners |
## 🔗 Linking a VRChat Group

To activate the ban system and Allowlist, you need to link a VRChat group to your server.

### Steps:

1. In your VRChat group, add the bot account **`novir studio`** and give it the **Moderator** role, or enable **Ban Members** permission manually
2. Copy the Group ID from its URL:  
   `https://vrchat.com/home/group/grp_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
3. In your Discord server, run the command:  
   `/setup group grp_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
4. The bot automatically verifies permissions and shows a confirmation message
5. After confirming ✅ — `/ban` and `/unban` commands will work directly in VRChat

> **Note:** If you see an error "Cannot link group", first make sure the bot has **Ban Members** permission in VRChat, then run the command again.

---

## 🎮 Connecting from Udon

You can connect a VRChat world directly to the platform to load the allowlist, gallery images, and custom messages.

---

### ℹ️ Overview

**Udon** is VRChat's built-in scripting system. It uses **`VRCUrl`** to fetch data from external sources via **String Downloader** or **Image Downloader**.

The platform provides ready-to-use endpoints:

| Endpoint | URL | Returns |
|----------|-----|----------|
| **Allowlist** | `/world/WORLD_KEY/allowlist.json` | List of linked player names |
| **All Images** | `/world/WORLD_KEY/images.json` | JSON list of all gallery images |
| **Landscape Images** | `/world/WORLD_KEY/images-landscape.json` | Landscape images only |
| **Portrait Images** | `/world/WORLD_KEY/images-portrait.json` | Portrait images only |
| **Current Image** | `/world/WORLD_KEY/current-image/landscape` | Direct image binary |

> To get your `WORLD_KEY`: open the dashboard at [novirlink.shop](https://novirlink.shop) → Settings.

---

### 📌 Loading the Allowlist (String Downloader)

Use this to load the allowed players list and check if a user has permission to enter the world.

**Required components in the world:**

| Component | Type | Purpose |
|-----------|------|---------|
| `VRC String Downloader` | Component | Fetches data as text |
| `UdonBehaviour` | Component | Processes data after load |
| `VRCUrl` | Variable | Stores the platform URL |

**Steps:**

1. Add `VRC String Downloader` component to a GameObject
2. Set the URL variable to:
   ```
   https://novirlink.shop/world/WORLD_KEY/allowlist.json
   ```
3. In your Udon script, call `DownloadString(url)` to start the download
4. In the `OnStringLoadSuccess` callback, you receive the data as a JSON string
5. Parse the JSON and search for the player's name inside the `allowList` array
6. If found → grant access or activate features / If not found → deny or do nothing

**JSON response format:**
```json
{
  "allowList": ["PlayerName1", "PlayerName2", "PlayerName3"],
  "updatedAt": "2026-04-26T12:00:00Z",
  "playerCount": 42
}
```

> **Important:** You must add `novirlink.shop` to the **Allowlisted URLs** list in your VRChat project settings (String Downloader URLs section).

---

### 🖼️ Displaying Gallery Images (Image Downloader)

You can upload images from the dashboard (banners, announcements, welcome art) and display them in your world automatically — no rebuild needed.

**Step 1: Upload images from the dashboard**

1. Open [novirlink.shop](https://novirlink.shop) and log in
2. Select your server → **Gallery** tab
3. Paste an image URL (from Imgur, Discord, or any CDN) and click **Add**
4. Choose orientation: **Landscape** or **Portrait**
5. You can reorder, enable, or disable each image individually

---

**Step 2: Load images in Udon**

Easiest method — load the current image directly as a binary:

| Component | Type | Purpose |
|-----------|------|---------|
| `VRC Image Downloader` | Component | Downloads image as Texture2D |
| `RawImage` / `MeshRenderer` | Component | Displays the image in the world |
| `TextureInfo` | Object | Texture settings |

**Steps:**

1. Set the URL variable to:
   ```
   https://novirlink.shop/world/WORLD_KEY/current-image/landscape
   ```
   Or for portrait:
   ```
   https://novirlink.shop/world/WORLD_KEY/current-image/portrait
   ```
2. In Udon, call `DownloadImage(url, textureInfo)` to start loading
3. In `OnImageLoadSuccess`, apply the Texture to `RawImage` or `Renderer.material`
4. In `OnImageLoadError`, show a fallback/placeholder image
5. The image updates automatically whenever you change it in the dashboard

---

**Advanced — Load a list of all images (for a slideshow):**

1. Use `VRC String Downloader` to fetch:
   ```
   https://novirlink.shop/world/WORLD_KEY/images-landscape.json
   ```
2. JSON response format:
   ```json
   {
     "worldKey": "abcdef1234567890",
     "orientation": "landscape",
     "imageCount": 3,
     "images": [
       { "url": "https://...", "label": "Welcome Banner" },
       { "url": "https://...", "label": "Event Poster" }
     ]
   }
   ```
3. In Udon, parse the JSON and call `DownloadImage(url)` for each image
4. Cycle through them with a timer or a button

> **Important:** Add `novirlink.shop` to your VRChat project's **Image Downloader URLs** allowlist.

---

### 💬 Displaying Platform Messages (String Downloader)

Write messages from the dashboard (announcements, rules, welcome text) and they appear in the world automatically — no world rebuild needed.

**Step 1: Add messages from the dashboard**

1. Open [novirlink.shop](https://novirlink.shop) and log in
2. Select your server → **Messages** tab
3. You have **2 slots (Slot 1 and Slot 2)** — each slot supports multiple messages
4. For each message: write the text (`text`) and set display duration (`duration`) in seconds
5. Messages update instantly after saving — no touching the Unity project

---

**Step 2: Fetch messages in Udon**

1. Use `VRC String Downloader` to fetch:
   ```
   https://novirlink.shop/world/WORLD_KEY/messages-1.json
   ```
   Or for slot 2:
   ```
   https://novirlink.shop/world/WORLD_KEY/messages-2.json
   ```
2. JSON response format:
   ```json
   {
     "slot": 1,
     "messageCount": 2,
     "messages": [
       { "text": "Welcome to the world!", "duration": 5 },
       { "text": "Enjoy your visit 🎉", "duration": 4 }
     ]
   }
   ```
3. In Udon, parse the JSON and loop through the array
4. Display each message in a `TextMeshPro` component and use `duration` as its display time (seconds)
5. Repeat the loop or trigger it on `OnPlayerJoined`

---

### ⚠️ Important Udon Requirements

| Requirement | Details |
|-------------|----------|
| **SDK** | VRChat SDK 3.x (Udon system) |
| **URL Allowlist** | Add `novirlink.shop` to both String + Image Downloader Allowlists |
| **Live data** | Data is always fresh — no local caching needed |
| **Rate limits** | Follow VRChat's request rules — don't fetch too frequently |
| **Privacy** | Data is public — don't store sensitive info in the allowlist |

---

## 🔒 Privacy & Data Security

**Your privacy is our priority.**

- ✅ All stored data (names, bans, links) is **private to your server only**
- ✅ **We never use your data** for any external purpose — no analytics, no sales, no third-party sharing
- ✅ Every server is isolated — server managers cannot see another server's data
- ✅ Your **WORLD_KEY** is private — do not share it with untrusted people
- ✅ You can delete all your data at any time from the dashboard
- ⚠️ Public-facing data (Allowlist, messages, images) is visible to anyone with your WORLD_KEY — do not put sensitive information in them

---

## ⚖️ NovirLink vs Other Platforms

| Feature | **NovirLink** | DisBridge | VRCX |
|---------|:-------------:|:---------:|:----:|
| Sync Discord roles to world permissions | ✅ | ✅ | ❌ |
| Whitelist (allowlist) from Discord | ✅ | ✅ | ❌ |
| Ban / Unban in VRChat from Discord | ✅ | ❌ | ❌ |
| Ban appeals system | ✅ | ❌ | ❌ |
| Web dashboard | ✅ | ❌ | ❌ |
| Upload images to world | ✅ | ❌ | ❌ |
| Custom messages for world | ✅ | ❌ | ❌ |
| Keypad / RoleTags / RoleBoard plugins | ❌ | ✅ | ❌ |
| Udon integration (VRChat worlds) | ✅ | ✅ | ❌ |
| Desktop application | ❌ | ❌ | ✅ |
| Price | 💰 **$13/mo** | 💰 **$25+** | Free |

> **DisBridge**: A Udon tool that syncs Discord roles to world permissions (doors, VIP areas, toggles) — no ban system, no appeals, no web dashboard. Starting at $25.  
> **VRCX**: A desktop app for tracking friends and worlds — no Discord integration, no ban management.

---

<div align="center">

---

**NovirLink** — Bridging Discord × VRChat since 2024  
[novirlink.shop](https://novirlink.shop) · Built with ❤️ by novir studio

---

</div>
