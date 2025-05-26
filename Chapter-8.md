---
layout: chapter
title: "Chapter 8: Beneath the Shelves — A Conversation About Databases"
---

> *"The right database is like the right foundation for a building — invisible, but everything depends on it."*

---

The sun was setting outside the office window, casting a warm glow over the whiteboard filled with entity diagrams and service definitions. Alex leaned back in his chair, a thoughtful look on his face.

**Alex:**
> So far, we’ve been using SQLite for our Bookshop app. It’s been smooth, but… is that what we’d use in production too?

Emma looked up from her laptop and smiled.

**Emma:**
> Great question. SQLite is perfect for development — it’s lightweight, file-based, and requires zero setup. But for production? We’ve got options.

Byte, who had been quietly sipping virtual coffee, perked up.

**Byte:**
> Let’s explore them! CAP supports multiple databases, and switching between them is easier than you think.

---

## 🧱 SQLite — The Developer’s Playground

**Emma:**
> Let’s start with what you already know — SQLite. It’s the default in CAP. You don’t even need to configure it explicitly, but here’s what it looks like in `package.json` or `.cdsrc.json`.

**Alex:**
> So that’s why it just worked when I ran `cds deploy`!

**Byte:**
> Exactly. It stores data in a local `.sqlite` file. Great for prototyping, but not for scaling.

```json
"cds": {
  "requires": {
    "db": {
      "kind": "sqlite",
      "model": ["db"]
    }
  }
}
```

---

## 🚀 SAP HANA — The Enterprise Powerhouse

**Emma:**
> Now, when you move to production — especially on SAP BTP — you’ll want SAP HANA. It’s fast, in-memory, and deeply integrated with SAP services.

She showed Alex the configuration:

**Byte:**
> And when you deploy to BTP, CAP automatically binds to the HANA service instance using environment variables. No need to hardcode credentials.

**Alex:**
> So I just run `cds deploy --to hana` and it knows what to do?

**Emma:**
> Exactly. And if you’re using an MTA project, it’ll even create the service instance for you.

```json
"cds": {
  "requires": {
    "db": {
      "kind": "hana",
      "model": ["db"]
    }
  }
}
```

---

## 🌍 PostgreSQL — The Open-Source Ally

**Alex:**
> What if I’m not on BTP? Can I use something like PostgreSQL?

**Byte:**
> You can! There’s a community adapter called `cds-pg`. It lets you use PostgreSQL with CAP.

Emma pulled up a sample config:

**Alex:**
> Nice! So I can use CAP even if I’m not in the SAP ecosystem.

**Emma:**
> Exactly. PostgreSQL is great for open-source projects or hybrid environments.

```json
"cds": {
  "requires": {
    "db": {
      "kind": "postgres",
      "model": ["db"],
      "credentials": {
        "host": "localhost",
        "port": 5432,
        "database": "bookshop",
        "user": "postgres",
        "password": "secret"
      }
    }
  }
}
```

---

## 🔄 Switching Between Databases

**Alex:**
> But switching between them… doesn’t that get messy?

**Byte:**
> Not at all. CAP supports profiles. You can define different setups for development, testing, and production.

Emma showed him how:

```json
"cds": {
  "profiles": {
    "development": {
      "requires": {
        "db": {
          "kind": "sqlite"
        }
      }
    },
    "production": {
      "requires": {
        "db": {
          "kind": "hana"
        }
      }
    }
  }
}
```

**Emma:**
> Then just run `cds deploy --profile production` to switch.

**Alex:**
> That’s super clean. So I can develop locally with SQLite and deploy to HANA without changing my code?

**Byte:**
> Exactly. CAP abstracts the database layer so you can focus on your domain model.

---

## 🧠 Wrapping Up

As the lights dimmed and the last lines of code were committed, Alex leaned back with a satisfied grin.

**Alex:**
> So CAP gives me the freedom to start small, scale big, and even go open-source if I want. That’s powerful.

**Emma:**
> And now you know what’s beneath the shelves of your Bookshop — a flexible, pluggable database layer.

**Byte:**
> Next stop: deploying to the cloud?

Alex nodded. “Let’s do it.”

---

[← Previous: Chapter 7](Chapter-7.md) | [Next: Chapter 9 →](Chapter-9.md)

[Back to Index](README.md)
