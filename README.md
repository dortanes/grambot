# 🤖 Telebot

**The declarative framework for building push-button Telegram bots with ease.**

Telebot is designed for developers who want to build complex, menu-driven Telegram bots without the boilerplate. It provides a fluent, declarative API for menus, automatic navigation, and streamlined conversations.

[![NPM Version](https://img.shields.io/npm/v/@superpackages/telebot.svg)](https://www.npmjs.com/package/@superpackages/telebot)
[![License](https://img.shields.io/npm/l/@superpackages/telebot.svg)](LICENSE)

## ✨ Features

- 🏗️ **Declarative Menus**: Define your bot's layout using a fluent builder API.
- 🔄 **Automatic Navigation**: Nested menus with built-in "Back" buttons.
- 💬 **Linear Conversations**: Collect user input easily with `ask()` and `form()`.
- 📝 **Single-Message Flow**: Edits the same message during interaction for a clean chat history.
- 🎨 **Button Styling**: Color your buttons (danger, success, primary) and add custom emoji icons.
- 🔡 **Type-Safe**: Written in TypeScript with full JSDoc documentation.
- 🌐 **Localization Support**: Built-in hooks for i18n.
- 🛠️ **Powered by Grammy**: Leverages the speed and reliability of the `grammy` framework.

## 🚀 Quick Start

### 1. Install

```bash
npm install @superpackages/telebot grammy
```

### 2. Create your bot

```typescript
import { Telebot } from "@superpackages/telebot";

// Define an action
const greetAction = Telebot.action(async ({ ctx, conversation }) => {
  const name = await conversation.ask("What is your name?");
  await ctx.reply(`Hello, ${name}! Welcome to the bot.`);
});

// Define a menu
const mainMenu = Telebot.menu((layout) => {
  layout.text("Welcome to the Bot! Choose an option:");

  layout.button("👋 Say Hello").primary().action(greetAction);
  layout.button("❌ Delete Account").danger().action(deleteAction);
  layout.button("✅ Confirm").success().action(confirmAction);
  layout.button("External Link").url("https://github.com/dortanes/telebot");
});

// Start the bot
const bot = Telebot.create({
  token: "YOUR_BOT_TOKEN",
  menu: mainMenu,
});

bot.start();
```

## 🎨 Button Styling

Telebot supports button colors and custom emoji icons (Telegram Bot API 9.4+).

```typescript
// Color styles
layout.button("Delete").danger();   // 🔴 Red
layout.button("Confirm").success(); // 🟢 Green
layout.button("Main").primary();    // 🔵 Blue

// Or use .style() directly
layout.button("Custom").style("danger");

// Custom emoji icon before button text
layout.button("Premium").icon("5368324170671202286");
```

> **Note:** Button colors require Telegram clients that support Bot API 9.4+ (February 2026+). Older clients will display normal buttons.

## 📖 Documentation

Explore the detailed guides:

- [Menus and Navigation](docs/menus.md) - Building layouts, rows, buttons, and styling.
- [Conversations and Forms](docs/conversations.md) - Collecting user input and complex data.
- [Actions and Triggers](docs/actions.md) - Logic, commands, and regex triggers.
- [State Management](docs/state.md) - Sessions, storage, and user resolution.
- [Advanced Patterns](docs/advanced.md) - I18n, custom storage, and manual rendering.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📜 License

[MIT](LICENSE)

---

<p align="center">
  Vibecoded with ❤️ by <a href="https://github.com/dortanes">dortanes</a>
</p>
