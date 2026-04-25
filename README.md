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

### 👑 لصاحب البوت
| الأمر | الوصف |
|-------|-------|
| `/owner stats` | إحصائيات البوت الكاملة |
| `/owner servers` | جميع السيرفرات المتصلة |
| `/owner broadcast <msg>` | رسالة لكل السيرفرات |
| `/owner link <user> <name>` | ربط يدوي |
| `/owner unlink <user>` | فك ربط يدوي |

---

## صفحات الموقع

| الصفحة | الرابط | لمن؟ |
|--------|--------|------|
| لوحة التحكم | `novirlink.shop` | أصحاب السيرفرات |
| تقديم استئناف | `novirlink.shop/appeal.html` | المستخدمون المحظورون |
| مراجعة الاستئنافات | `novirlink.shop/appeals-review.html?guildId=ID` | أصحاب السيرفرات |

---

## التقنيات المستخدمة

```
Backend   →  Node.js + Express.js
Bot       →  Discord.js v14
Database  →  SQLite (sql.js)
Auth      →  Discord OAuth2
Hosting   →  AWS Lightsail
```

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

### 👑 For Bot Owner
| Command | Description |
|---------|-------------|
| `/owner stats` | Full bot statistics |
| `/owner servers` | All connected servers |
| `/owner broadcast <msg>` | Message all servers |
| `/owner link <user> <name>` | Force link a user |
| `/owner unlink <user>` | Force unlink a user |

---

## Website Pages

| Page | URL | For |
|------|-----|-----|
| Dashboard | `novirlink.shop` | Server owners |
| Submit appeal | `novirlink.shop/appeal.html` | Banned users |
| Review appeals | `novirlink.shop/appeals-review.html?guildId=ID` | Server owners |
| Owner panel | `novirlink.shop/owner.html` | Bot owner only |

---

## Tech Stack

```
Backend   →  Node.js + Express.js
Bot       →  Discord.js v14
Database  →  SQLite (sql.js — in-memory + file persistence)
Auth      →  Discord OAuth2 + Bearer Token
Hosting   →  AWS Lightsail (Ubuntu)
Proxy     →  Nginx (reverse proxy to port 3010)
Process   →  PM2
```

---
---

<br/>
<br/>

---

# 🛠️ Technical Documentation — التوثيق التقني

---

## 📁 Project Structure — هيكل المشروع

```
novirlink/
├── src/
│   ├── index.js                    ← Entry point (Express + Discord bot)
│   ├── api/
│   │   ├── index.js                ← API router mount
│   │   └── routes/
│   │       ├── auth.js             ← Discord OAuth2, session auth
│   │       └── dashboard.js        ← All API endpoints (3000+ lines)
│   ├── bot/
│   │   ├── index.js                ← Bot initialization, event loading
│   │   ├── commands/
│   │   │   ├── admin.js            ← /admin command
│   │   │   ├── ban.js              ← /ban command
│   │   │   ├── banlist.js          ← /banlist command
│   │   │   ├── blacklist.js        ← /blacklist command
│   │   │   ├── link.js             ← /link command
│   │   │   ├── music.js            ← /music command
│   │   │   ├── owner.js            ← /owner command (bot owner only)
│   │   │   ├── ping.js             ← /ping command
│   │   │   ├── setup.js            ← /setup command
│   │   │   ├── stats.js            ← /stats command
│   │   │   ├── unban.js            ← /unban command
│   │   │   └── unlink.js           ← /unlink command
│   │   ├── events/
│   │   │   └── guildMemberUpdate.js ← Role change detection → auto sync
│   │   └── utils/
│   │       ├── auto-unban.js       ← Timer-based unban scheduler
│   │       ├── music.js            ← Music utilities
│   │       └── sync.js             ← Allowlist sync logic
│   ├── db/
│   │   ├── index.js                ← sql.js init, load/save to disk
│   │   ├── queries.js              ← All DB functions
│   │   └── migrations/
│   │       ├── 001_create_worlds.sql
│   │       ├── 002_create_links.sql
│   │       ├── 003_create_admins.sql
│   │       ├── 003_create_blacklist.sql
│   │       ├── 004_add_vrchat_group.sql
│   │       ├── 004_create_bans.sql
│   │       ├── 005_add_group_id.sql
│   │       ├── 006_add_announcement_channel.sql
│   │       ├── 007_add_banned_by_tag.sql
│   │       └── 007_create_server_logs.sql
│   └── utils/
│       ├── logger.js               ← Logging utilities
│       ├── subscription.js         ← Subscription management
│       ├── validation.js           ← Input sanitization & validation
│       └── vrchat-api.js           ← All VRChat API calls (~1200 lines)
├── public/
│   ├── index.html                  ← Main user dashboard
│   ├── owner.html                  ← Bot owner control panel
│   ├── appeal.html                 ← Ban appeal submission page
│   ├── app.js                      ← Client-side JS for index.html
│   └── styles.css                  ← Shared CSS
├── data/
│   ├── cookies.txt                 ← VRChat session cookies
│   └── vrchat-session.json         ← VRChat session data
├── deploy/
│   ├── nginx.conf                  ← Production nginx config
│   ├── novirlink.service           ← Systemd service file
│   └── WINDOWS_DEPLOYMENT.md       ← Deployment guide
├── scripts/
│   ├── register-commands.js        ← Register Discord slash commands
│   └── migrate.js                  ← Run DB migrations
├── package.json
└── ecosystem.config.cjs            ← PM2 config
```

---

## 🗄️ Database Schema — هيكل قاعدة البيانات

> **Engine:** SQLite via `sql.js` — loaded into memory on startup, saved to disk every 60 seconds and on graceful shutdown.
> **File path:** `data/novirlink.db`

---

### Table: `worlds`
Stores one row per Discord server (subscription).

```sql
CREATE TABLE worlds (
    id                     INTEGER PRIMARY KEY AUTOINCREMENT,
    guild_id               TEXT    UNIQUE NOT NULL,   -- Discord server ID
    owner_id               TEXT    NOT NULL,          -- Discord user ID of server owner
    world_key              TEXT    UNIQUE NOT NULL,   -- Unique URL key (UUID)
    vrchat_group_id        TEXT,                      -- Linked VRChat group ID (grp_xxx)
    required_role_id       TEXT,                      -- Required Discord role to /link
    announcement_channel_id TEXT,                     -- Channel for ban notifications
    created_at             DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at             DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

### Table: `links`
Stores VRChat ↔ Discord bindings per server.

```sql
CREATE TABLE links (
    id              INTEGER PRIMARY KEY AUTOINCREMENT,
    guild_id        TEXT    NOT NULL,     -- Discord server ID
    discord_user_id TEXT    NOT NULL,     -- Discord user ID
    vrchat_name     TEXT    NOT NULL,     -- VRChat display name
    active          INTEGER DEFAULT 1,   -- 1 = active, 0 = removed
    created_at      DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at      DATETIME DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(guild_id, discord_user_id)
);
```

---

### Table: `bans`
Stores ban records per server.

```sql
CREATE TABLE bans (
    id              INTEGER PRIMARY KEY AUTOINCREMENT,
    guild_id        TEXT    NOT NULL,     -- Discord server ID
    vrchat_name     TEXT    NOT NULL,     -- Banned VRChat name
    reason          TEXT,                 -- Ban reason
    duration        TEXT,                 -- "1h", "1d", "7d", "30d", "permanent"
    banned_by       TEXT,                 -- Discord user ID of banner
    banned_by_tag   TEXT,                 -- Discord tag (username#0000) of banner
    expires_at      DATETIME,             -- NULL = permanent
    active          INTEGER DEFAULT 1,   -- 1 = still banned, 0 = unbanned
    created_at      DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

### Table: `admins`
Stores per-server admin permissions.

```sql
CREATE TABLE admins (
    id              INTEGER PRIMARY KEY AUTOINCREMENT,
    guild_id        TEXT    NOT NULL,
    discord_user_id TEXT    NOT NULL,
    added_by        TEXT,
    created_at      DATETIME DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(guild_id, discord_user_id)
);
```

---

### Table: `blacklist`
Global blacklist (blocked from using /link on any server).

```sql
CREATE TABLE blacklist (
    id              INTEGER PRIMARY KEY AUTOINCREMENT,
    vrchat_name     TEXT    UNIQUE NOT NULL,
    reason          TEXT,
    added_by        TEXT,
    created_at      DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

### Table: `server_logs`
Audit log for all actions.

```sql
CREATE TABLE server_logs (
    id              INTEGER PRIMARY KEY AUTOINCREMENT,
    guild_id        TEXT    NOT NULL,
    action          TEXT    NOT NULL,   -- e.g. 'ban', 'link', 'admin_add'
    details         TEXT,               -- Human-readable detail string
    user_id         TEXT,               -- Who performed the action
    user_name       TEXT,               -- Username for display
    target_name     TEXT,               -- Who was affected
    created_at      DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

**Action values:**

| Value | Meaning |
|-------|---------|
| `ban` | Player banned |
| `unban` | Player unbanned |
| `auto_unban` | Auto-unbanned after expiry |
| `link` | User linked VRChat name |
| `unlink` | User unlinked |
| `web_link` | Linked via web dashboard |
| `owner_link` | Force-linked by owner |
| `owner_unlink` | Force-unlinked by owner |
| `owner_unlink_group` | Owner removed VRChat group |
| `admin_add` | Admin added |
| `admin_remove` | Admin removed |
| `link_edit` | User edited their linked name |
| `owner_dm` | Owner sent a DM |
| `settings` | Settings changed |
| `gallery_settings` | Gallery settings changed |

---

### Table: `ban_appeals`
Stores ban appeal submissions.

```sql
CREATE TABLE ban_appeals (
    id               INTEGER PRIMARY KEY AUTOINCREMENT,
    guild_id         TEXT    NOT NULL,        -- Server the ban is from
    discord_user_id  TEXT    NOT NULL,        -- Appealing user's Discord ID
    discord_username TEXT,                    -- Discord display name
    discord_avatar   TEXT,                    -- Avatar URL for display
    vrchat_name      TEXT    NOT NULL,        -- VRChat name (from linked account)
    reason           TEXT    NOT NULL,        -- Appeal reason written by user
    status           TEXT    DEFAULT 'pending',  -- 'pending', 'approved', 'rejected'
    review_note      TEXT,                    -- Admin's note to user
    reviewed_by      TEXT,                    -- Admin Discord ID
    reviewed_by_tag  TEXT,                    -- Admin tag for display
    reviewed_at      DATETIME,
    created_at       DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

### Table: `global_profiles`
Global username mapping across all servers.

```sql
CREATE TABLE global_profiles (
    id               INTEGER PRIMARY KEY AUTOINCREMENT,
    discord_user_id  TEXT    UNIQUE NOT NULL,
    vrchat_name      TEXT    NOT NULL,
    last_changed_at  DATETIME DEFAULT CURRENT_TIMESTAMP,
    created_at       DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

## 🔌 API Reference — توثيق الـ API

> **Base URL:** `https://novirlink.shop/api`  
> **Auth:** Session cookie OR `Authorization: Bearer <token>` header  
> **Token:** Obtained via Discord OAuth2, stored in `localStorage`

---

### 🔐 Auth Endpoints

#### `GET /s/discord`
Redirect to Discord OAuth2 login.

**Query params:**
- `return_url` — Where to redirect after login

---

#### `GET /s/me`
Check current auth status.

**Response:**
```json
{
  "id": "714077322516365414",
  "username": "username",
  "avatar": "avatar_hash",
  "isOwner": true
}
```

---

#### `GET /s/token`
Exchange session for Bearer token (used by web pages).

**Response:**
```json
{ "token": "eyJhbGci..." }
```

---

### 🌍 World / Allowlist Endpoints

#### `GET /world/:worldKey/allowlist.json`
Public allowlist endpoint — used directly in VRChat world.

**No auth required.**

**Response:**
```json
{
  "allowList": ["PlayerName1", "PlayerName2"],
  "updatedAt": "2026-04-26T12:00:00Z",
  "playerCount": 42
}
```

---

#### `GET /world/global/allowlist.json`
Global allowlist — all linked players across all servers.

**No auth required.**

---

### 👤 User Dashboard Endpoints

#### `GET /api/my/world`
Get current user's server info.

**Auth required.**

---

#### `GET /api/my/links`
Get all VRChat names linked by the current user.

---

#### `GET /api/server/:guildId/links`
Get all active links (allowlist) for a server.

**Auth required.** Admin or server owner.

---

#### `POST /api/server/:guildId/group`
Link a VRChat group to a server.

**Auth required.** Server owner or bot owner.

**Body:**
```json
{ "groupId": "grp_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" }
```

**Response:**
```json
{ "success": true, "groupName": "My VRChat Group", "groupId": "grp_xxx..." }
```

**Errors:**
- `400` — Invalid group ID format (must start with `grp_`)
- `400` — VRChat API not connected
- `400` — Bot cannot manage bans in group (no permission)
- `409` — Group already linked to another server

---

#### `DELETE /api/server/:guildId/group`
Unlink the VRChat group from a server.

**Auth required.**

---

#### `POST /api/server/:guildId/channel`
Set announcement channel.

**Body:**
```json
{ "channelId": "123456789012345678" }
```

---

#### `POST /api/server/:guildId/rotate-key`
Generate a new `world_key` (new allowlist URL).

**Auth required.**

---

### 🚫 Ban Endpoints

#### `GET /api/server/:guildId/bans`
Get all bans for a server.

#### `POST /api/server/:guildId/ban`
Create a new ban.

**Body:**
```json
{
  "vrchatName": "PlayerName",
  "reason": "reason text",
  "duration": "7d"
}
```

**Duration values:** `1h` · `12h` · `1d` · `3d` · `7d` · `14d` · `30d` · `permanent`

#### `DELETE /api/server/:guildId/ban/:banId`
Remove a ban.

---

### ⚖️ Appeal Endpoints

#### `GET /api/appeal/my-link`
Get current user's linked VRChat name (for pre-filling appeal form).

#### `GET /api/appeal/my-bans?guildId=...`
Get ban info for the current user in a specific server.

#### `POST /api/appeal/submit`
Submit a ban appeal.

**Body:**
```json
{
  "guildId": "discord_server_id",
  "reason": "appeal reason text"
}
```

#### `GET /api/appeal/my-appeals`
Get all appeals submitted by the current user.

#### `GET /api/server/:guildId/appeals`
Get all appeals for a server (admin view).

**Query params:** `page`, `limit`, `status` (`pending`/`approved`/`rejected`), `search`

#### `PUT /api/server/:guildId/appeals/:appealId`
Review an appeal (approve or reject).

**Body:**
```json
{
  "status": "approved",
  "reviewNote": "optional note to user"
}
```

When `status = "approved"`:
- Bans are removed from the database
- VRChat group unban is triggered automatically

---

### 👑 Owner-Only Endpoints

#### `GET /api/owner/full-stats`
Complete platform statistics — all servers, counts, VRChat status.

#### `GET /api/owner/bans`
All bans across all servers.

#### `GET /api/owner/logs`
All activity logs across all servers.

**Query params:** `page`, `limit`, `action`, `search`

#### `GET /api/owner/groups`
All servers with linked VRChat groups.

#### `DELETE /api/owner/group-link/:guildId`
Force-remove a VRChat group from a server.

#### `GET /api/owner/server/:guildId/details`
Full detail for one server (players, bans, admins, settings).

#### `POST /api/owner/force-link`
Force-link a Discord user to a VRChat name on a specific server.

**Body:**
```json
{
  "discordUserId": "...",
  "vrchatName": "PlayerName",
  "guildId": "..."
}
```

#### `DELETE /api/owner/force-unlink/:guildId/:discordUserId`
Force-unlink.

#### `GET /api/owner/all-links`
All links across all servers (paginated, searchable).

#### `GET /api/owner/appeals`
All appeals across all servers.

#### `PUT /api/owner/appeals/:appealId`
Review any appeal (owner can review any server's appeals).

#### `POST /api/owner/send-message`
Send a DM to a server's owner/admins via Discord bot.

**Body:**
```json
{
  "guildId": "...",
  "recipientType": "both",
  "message": "Hello!"
}
```

#### `POST /api/owner/broadcast`
Send DM to all servers.

#### `POST /api/owner/backup-now`
Trigger a manual database backup.

---

## 🔑 Environment Variables — متغيرات البيئة

All configured in `.env` at the project root.

```env
# ═══════════════════════════════════════
# Discord Bot
# ═══════════════════════════════════════
DISCORD_TOKEN=                  # Bot token from Discord Developer Portal
DISCORD_CLIENT_ID=              # Application Client ID
DISCORD_CLIENT_SECRET=          # OAuth2 secret (for web login)
DISCORD_REDIRECT_URI=           # OAuth2 callback URL
                                # e.g. https://novirlink.shop/s/discord/callback

# ═══════════════════════════════════════
# Server IDs
# ═══════════════════════════════════════
MAIN_GUILD_ID=                  # The "home" Discord server ID
SUBSCRIPTION_ROLE_ID=           # Role that grants subscription access

# ═══════════════════════════════════════
# Bot Owner
# ═══════════════════════════════════════
BOT_OWNER_ID=                   # Main owner Discord user ID
BOT_CO_OWNER_ID=                # Co-owner Discord user ID (optional)

# ═══════════════════════════════════════
# App
# ═══════════════════════════════════════
BASE_URL=https://novirlink.shop  # Public base URL (no trailing slash)
PORT=3010                        # Internal port (Nginx proxies to this)
SESSION_SECRET=                  # Express session secret (random long string)
JWT_SECRET=                      # JWT signing secret (for Bearer tokens)

# ═══════════════════════════════════════
# Database
# ═══════════════════════════════════════
DB_PATH=./data/novirlink.db      # SQLite file path

# ═══════════════════════════════════════
# VRChat (auto-managed by login script)
# ═══════════════════════════════════════
VRCHAT_USERNAME=                 # VRChat account username/email
VRCHAT_PASSWORD=                 # VRChat account password
```

---

## 🌐 VRChat API Integration

The platform uses VRChat's unofficial REST API directly.

**Base URL:** `https://api.vrchat.cloud/api/1`

### Authentication
- Login via `POST /auth/user` with credentials + TOTP
- Session stored in cookies (`auth`, `apiKey`, `twoFactorAuth`)
- Cookie file: `data/cookies.txt`

### Key Operations Used

| Operation | VRChat Endpoint | Used For |
|-----------|----------------|----------|
| Search user | `GET /users?search=name` | Verify name on `/link` |
| Get user by ID | `GET /users/:id` | Profile lookup |
| Get group info | `GET /groups/:groupId` | Validate group on `/setup group` |
| Get group members | `GET /groups/:groupId/members` | Sync checks |
| Get group bans | `GET /groups/:groupId/bans` | Ban list sync |
| Ban user from group | `POST /groups/:groupId/bans` | Auto-ban on `/ban` |
| Unban from group | `DELETE /groups/:groupId/bans/:userId` | Auto-unban |
| Check my member | `GET /groups/:groupId` → `myMember` field | Permission check |
| Request join group | `POST /groups/:groupId/join` | Auto-join on setup |

### Permission Check
Before linking a group, the bot checks if its VRChat account has `group-bans-manage` permission or is group owner:

```javascript
const hasModPermission =
  groupInfo.myMember.isOwner ||
  groupInfo.myMember.permissions?.includes('group-bans-manage');
```

If the bot lacks permission, `/setup group` returns instructions to grant `Moderator` role in VRChat.

### Rate Limiting
- VRChat API enforces aggressive rate limits
- The platform includes internal caching (`cacheSet`/`cacheGet`) with TTLs per endpoint type
- Group info cached for 5 minutes
- User lookups cached for 2 minutes

---

## 🔄 Sync System

### Role-Based Auto-Sync
When a Discord member's role changes (`guildMemberUpdate` event):

```
Role REMOVED  →  Check if required role → Deactivate link → Remove from allowlist
Role ADDED    →  Check if already linked → Re-activate link → Add to allowlist
```

### Allowlist Generation
The `/world/:worldKey/allowlist.json` endpoint is live — it queries the database on every request and returns all active linked names for that server.

No caching needed because the file is fetched by VRChat on world entry.

### Auto-Unban Scheduler
Runs every 5 minutes. Checks all bans where `expires_at < NOW()` and `active = 1`:
1. Marks ban as `active = 0` in database
2. Calls VRChat API to unban
3. Logs the action to `server_logs`

---

## 🔐 Authentication Flow

### Web Dashboard Login
```
1. User visits novirlink.shop
2. Clicks "Login with Discord"
3. Redirected to /s/discord
4. Discord OAuth2 → callback to /s/discord/callback
5. Server exchanges code for Discord user info
6. Session created (express-session)
7. JWT token generated → saved in localStorage
8. All subsequent requests send: Authorization: Bearer <token>
```

### Access Levels

| Level | Who | Can Access |
|-------|-----|-----------|
| **Public** | Anyone | Allowlist JSON, global allowlist |
| **User** | Logged-in Discord user | Own profile, own links, appeals |
| **Server Admin** | Has admin record in DB | Server dashboard, bans, members |
| **Server Owner** | Created the server record | All server settings + admin mgmt |
| **Bot Owner** | `BOT_OWNER_ID` env var | Everything — owner.html panel |

---

## 🚀 Deployment — النشر

### Server Info
- **Provider:** AWS Lightsail
- **OS:** Ubuntu 22.04
- **IP:** `13.232.225.51` (ap-south-1)
- **SSH Key:** `LightsailDefaultKey-ap-south-1.pem`
- **App path:** `/home/ubuntu/novirlink/`
- **Process manager:** PM2 (app name: `novirlink`, id: 0)
- **Port:** `3010` (internal) → Nginx proxies from 80/443

### Deploy Commands

```powershell
# From local Windows machine (project root)
$SSH_KEY = "LightsailDefaultKey-ap-south-1.pem"
$REMOTE  = "ubuntu@13.232.225.51"
$DEST    = "/home/ubuntu/novirlink"

# Upload a specific file
scp -i $SSH_KEY "public/owner.html" "${REMOTE}:${DEST}/public/owner.html"

# Upload multiple files
scp -i $SSH_KEY "src/api/routes/dashboard.js" "${REMOTE}:${DEST}/src/api/routes/dashboard.js"
scp -i $SSH_KEY "public/owner.html" "${REMOTE}:${DEST}/public/owner.html"

# Restart app
ssh -i $SSH_KEY $REMOTE "pm2 restart novirlink"

# View logs
ssh -i $SSH_KEY $REMOTE "pm2 logs novirlink --lines 50"
```

### PM2 Config (`ecosystem.config.cjs`)
```javascript
module.exports = {
  apps: [{
    name: 'novirlink',
    script: 'src/index.js',
    interpreter: 'node',
    env: {
      NODE_ENV: 'production',
      PORT: 3010
    },
    restart_delay: 3000,
    max_memory_restart: '500M'
  }]
};
```

### Nginx Config (simplified)
```nginx
server {
    listen 443 ssl;
    server_name novirlink.shop;

    location / {
        proxy_pass         http://localhost:3010;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection 'upgrade';
        proxy_set_header   Host $host;
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_cache_bypass $http_upgrade;
    }
}
```

---

## 🧪 Useful Scripts

Located in `scripts/`:

| Script | Command | Purpose |
|--------|---------|---------|
| `register-commands.js` | `node scripts/register-commands.js` | Register slash commands with Discord |
| `delete-commands.js` | `node scripts/delete-commands.js` | Remove all slash commands |
| `migrate.js` | `node scripts/migrate.js` | Run pending DB migrations |
| `check-bans.js` | `node scripts/check-bans.js` | Debug ban records |
| `check-sessions.js` | `node scripts/check-sessions.js` | Debug active sessions |
| `fix-bans.js` | `node scripts/fix-bans.js` | Fix ban inconsistencies |
| `fix-ratelimit.js` | `node scripts/fix-ratelimit.js` | Reset VRChat rate limit state |

---

## 🐛 Common Issues & Fixes

### VRChat Group Linking Fails
**Symptom:** `/setup group` says "لا يمكن ربط القروب"

**Fix:**
1. Go to the VRChat group
2. Find the bot account (`novir studio`)
3. Give it the **Moderator** role or enable **Ban Members** permission
4. Run `/setup group <id>` again

---

### VRChat API Disconnected
**Symptom:** VRChat shows as `❌ غير متصل` in owner panel

**Fix:**
```bash
# SSH into server
ssh -i LightsailDefaultKey-ap-south-1.pem ubuntu@13.232.225.51

# Run the interactive login script
node /home/ubuntu/novirlink/local-vrc-login.mjs

# Follow the prompts (email, password, 2FA if needed)
# Then restart the app
pm2 restart novirlink
```

---

### "Cannot send messages to this user" DM Error
**Cause:** Discord blocks DMs when the bot shares no mutual server with the user (because the user was banned from the server).

**Expected behavior:** The appeal system uses an **in-page banner** instead of DMs to notify users of appeal decisions. This is intentional — DMs are best-effort only.

---

### Allowlist Not Updating
**Symptom:** VRChat world still shows old names

**Fix:** The allowlist endpoint is live — check:
1. Is the bot running? `pm2 status`
2. Is the world using the correct URL from `/setup info`?
3. Did the VRChat world reload the allowlist? (Some worlds cache it)

---

### Group Already Linked Error (`409`)
**Cause:** The `grp_xxx` ID is already stored in another server's `worlds` record.

**Fix (owner only):**
1. Open `owner.html` → Groups tab
2. Find the server that has this group
3. Click **فصل القروب** to unlink it
4. Then link it to the new server

---

## 📊 Owner Panel — لوحة تحكم المالك

URL: `novirlink.shop/owner.html`  
Access: `BOT_OWNER_ID` or `BOT_CO_OWNER_ID` only.

### Tabs Available

| Tab | Arabic | What it shows |
|-----|--------|--------------|
| 🚫 Bans | الحظورات | All bans across all servers, force-unban button |
| 📋 Logs | السجل | Full activity log, filterable by action type |
| 🖥️ Servers | السيرفرات | All servers grid with stats + group link button |
| 📈 Analytics | التحليلات | Daily charts, growth rates, MVP servers |
| 🔗 Groups | القروبات | All linked VRChat groups, unlink option |
| 📦 Subscriptions | الاشتراكات | All subscriptions, cancel option |
| 🔗 Links | الربط | Force link/unlink users, global allowlist URL |
| ⚖️ Appeals | الاستئنافات | All appeals from all servers, review any |
| ✉️ Messages | الرسائل | Send DMs to server owners/admins, message history |
| ⚙️ System | النظام | VRChat status, uptime, memory, database backups |

### Auto-Refresh
The active tab auto-refreshes every **15 seconds**. When you switch tabs the refresh timer resets to follow the new tab.

---

## 🔗 Linking a VRChat Group (Step-by-Step)

### Method 1 — Discord Command
```
/setup group grp_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
1. Bot checks if it's a member of the group
2. If not → sends join request automatically
3. Checks if bot has `group-bans-manage` permission
4. If not → shows instructions to grant Moderator role
5. Shows confirmation button with group info
6. After confirmation → group is saved and future `/ban` commands work

### Method 2 — Owner Panel (Web)
1. Open `novirlink.shop/owner.html`
2. Go to **🖥️ السيرفرات** tab
3. Find the server you want
4. Click **🎮 ربط قروب**
5. Enter the group ID (`grp_xxx...`)
6. Click **🔗 ربط القروب**
7. If success → modal closes and server card updates

> The group ID can be found in the VRChat group's URL:  
> `https://vrchat.com/home/group/grp_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`

---

## ⚡ Performance Notes

- **Database:** SQLite in-memory — extremely fast reads, saved to disk periodically
- **VRChat API:** Responses cached in-memory (groupInfo: 5min, userSearch: 2min)
- **Allowlist endpoint:** No caching — always fresh from DB
- **Static files:** Served directly by Nginx (HTML/CSS/JS bypass Node.js)
- **Auto-unban scheduler:** Runs every 5 minutes using `setInterval`

---

## 🛡️ Security

- All inputs sanitized via `sanitize()` helper (strips XSS)
- Discord snowflake IDs validated with `isValidSnowflake()` before DB queries
- Session secret and JWT secret stored in `.env` (not in code)
- `requireOwner` middleware blocks all owner endpoints from non-owners
- `requireServerAccess` middleware ensures users can only manage their own servers
- OAuth2 tokens never stored in the database — sessions only
- All parameterized SQL (sql.js `run()` with bound params) — no SQL injection

---

<div align="center">

---

**NovirLink** — Bridging Discord & VRChat since 2024  
[novirlink.shop](https://novirlink.shop) · Built with ❤️ by novir studio

---

</div>

- ✅ Banned user sees their ban reason automatically
- ✅ Independent review page per server
- ✅ Approval auto-unbans from VRChat
- ✅ Track appeal status from the same page

---

### 📊 Web Dashboard
Full web interface at [novirlink.shop](https://novirlink.shop)

| Section | What it offers |
|---------|---------------|
| **Members** | View linked members, search, remove |
| **Bans** | Add, lift, view ban list |
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
| `/setup enable` | Enable the system in the server |
| `/setup role <role>` | Set the required role |
| `/setup group <id>` | Link a VRChat group |
| `/setup channel <channel>` | Set notification channel |
| `/setup info` | Current setup info |
| `/unlink <user>` | Remove a member's link |
| `/ban <name> <duration> <reason>` | Ban a player |
| `/unban <name>` | Unban a player |
| `/banlist` | View ban list |
| `/blacklist add/remove/list` | Manage blacklist |
| `/admin add/remove/list` | Manage admins |
| `/stats` | Server statistics |

### 👑 For Bot Owner
| Command | Description |
|---------|-------------|
| `/owner stats` | Full bot statistics |
| `/owner servers` | All connected servers |
| `/owner broadcast <msg>` | Message to all servers |
| `/owner link <user> <name>` | Manual link |
| `/owner unlink <user>` | Manual unlink |

---

## Website Pages

| Page | URL | For whom? |
|------|-----|-----------|
| Dashboard | `novirlink.shop` | Server owners |
| Submit Appeal | `novirlink.shop/appeal.html` | Banned users |
| Review Appeals | `novirlink.shop/appeals-review.html?guildId=ID` | Server owners |

---

## Tech Stack

```
Backend   →  Node.js + Express.js
Bot       →  Discord.js v14
Database  →  SQLite (sql.js)
Auth      →  Discord OAuth2
Hosting   →  AWS Lightsail
```

---

<div align="center">

<br/>

**Built with ❤️**

[![Website](https://img.shields.io/badge/🌐_novirlink.shop-Visit_Now-b47aff?style=for-the-badge)](https://novirlink.shop)

![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=flat-square&logo=node.js&logoColor=white)
![Discord.js](https://img.shields.io/badge/Discord.js-v14-5865F2?style=flat-square&logo=discord&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

</div>
