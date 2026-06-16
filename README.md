<table>
<tr>
<td>

## Grambot

[![NPM Version](https://img.shields.io/npm/v/grambot)](https://www.npmjs.com/package/grambot) [![License](https://img.shields.io/npm/l/grambot)](LICENSE)

</td>
</tr>
</table>

A declarative framework for building menu-driven Telegram bots. No boilerplate — just menus, buttons, and conversations.

[Install](#-install) • [Quick Start](#-quick-start) • [Documentation](#-documentation) • [Releases](https://github.com/dortanes/grambot/releases)

---

## 📦 Install

```bash
npm install grambot grammy
```

## 🚀 Quick Start

```typescript
import { Grambot } from "grambot";

const greetAction = Grambot.action(async ({ conversation }) => {
  const name = await conversation.ask("What is your name?");
  await conversation.say(`Hello, ${name}!`);
});

const mainMenu = Grambot.menu((layout) => {
  layout.text("Welcome! Choose an option:");
  layout.button("👋 Say Hello").primary().action(greetAction);
  layout.button("🌐 Website").url("https://github.com/dortanes/grambot");
});

const bot = Grambot.create({
  token: process.env.BOT_TOKEN!,
  menu: mainMenu,
});

bot.start();
```

## ✨ Features

|     | Feature                 | Description                                              |
| --- | ----------------------- | -------------------------------------------------------- |
| 🏗️  | **Declarative Menus**   | Define layouts with a fluent builder API                 |
| 🔄  | **Auto Navigation**     | Nested menus with built-in "Back" buttons                |
| 💬  | **Conversations**       | Collect input with `ask()` and `form()`                  |
| 📝  | **Single-Message Flow** | Edits one message for a clean chat history               |
| 🎨  | **Button Styling**      | Colors (danger, success, primary) and custom emoji icons |
| 🛡️  | **Error Handling**      | Built-in error boundary — no crashes                     |
| 🌐  | **i18n Support**        | Localization hooks for all internal strings              |
| 🔡  | **Type-Safe**           | Full TypeScript with JSDoc                               |

## 🎨 Button Styling

Color your buttons and add custom emoji icons (Bot API 9.4+):

```typescript
layout.button("Delete").danger(); // 🔴 Red
layout.button("Confirm").success(); // 🟢 Green
layout.button("Highlight").primary(); // 🔵 Blue

layout.button("VIP").icon("custom_emoji_id");
```

## ⚙️ Configuration

```typescript
const bot = Grambot.create({
  token: "BOT_TOKEN",
  menu: mainMenu,

  // Resolve user data from DB on every update
  resolveUser: async (ctx) => {
    return await db.users.find(ctx.from.id);
  },

  // Localize internal strings
  translator: (key, ctx) => i18n.t(ctx.from.language_code, key),

  // Custom error handler (default: console.error)
  onError: (error, ctx) => {
    logger.error("Bot error", { error, chatId: ctx.chat?.id });
  },
});
```

## 📖 Documentation

| Guide                                            | Description                                 |
| ------------------------------------------------ | ------------------------------------------- |
| [Menus and Navigation](docs/menus.md)            | Layouts, rows, buttons, styling, pagination |
| [Conversations and Forms](docs/conversations.md) | User input, validation, multi-step forms    |
| [Actions and Triggers](docs/actions.md)          | Commands, regex, inline handlers            |
| [State Management](docs/state.md)                | Sessions, storage adapters, user resolution |
| [Advanced Patterns](docs/advanced.md)            | i18n, webhooks, manual rendering            |

## Development

```bash
git clone https://github.com/dortanes/grambot.git
cd grambot

npm install

npm run build

BOT_TOKEN=your_token npm run start:example
```

## License

[MIT](LICENSE)

<p align="center" style="margin-top: 40px">
  Made with ❤️ by <a href="https://github.com/dortanes">dortanes</a><br/>
  (pls star this repo if you find it useful)
</p>
