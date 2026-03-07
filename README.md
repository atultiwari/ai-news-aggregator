<div align="center">

# 🏥 AI Healthcare News Aggregator

**Real-time AI & Healthcare news — aggregating the best sources in medicine, pathology, and laboratory science**

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Node.js](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen?logo=node.js)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue?logo=typescript)](https://www.typescriptlang.org/)

[🌐 Live Demo](https://atultiwari.github.io/ai-news-aggregator/) · [📝 Changelog](./CHANGELOG.md) · [📡 Sources](./recommended-sources.md)

</div>

---

## ✨ Key Features

<table>
<tr>
<td width="50%">

### 📡 Multi-Source Aggregation
Aggregates from **49+ curated sources** including top AI labs, healthcare media, pathology journals, and research preprints.

### 🏥 Healthcare Specialty Filtering
Filter news by **21 medical specialties** — Pathology, Radiology, Oncology, Surgery, Medicine, Microbiology, Biochemistry, and more.

### 🧠 Smart Filtering
AI-relevance keyword matching filters out noise and surfaces healthcare-related AI content from general tech feeds.

</td>
<td width="50%">

### ⚡ Automatic Updates
GitHub Actions fetches data every 2 hours, keeping the feed current.

### 🎨 Modern Web Interface
Built with React + TypeScript + Tailwind CSS. Supports dark mode, search, multi-dimension filtering, favorites, and reading history.

### 📦 Structured Data
Outputs standardized JSON files for easy downstream analysis and integration.

</td>
</tr>
</table>

---

## 🏥 Healthcare Specialty Tags

The aggregator automatically tags articles with relevant medical specialties based on title keyword matching. You can filter by any combination of:

| Tag | Specialties |
|:----|:------------|
| 🔬 | Pathology, Digital Pathology, Histopathology |
| 📷 | Radiology, Medical Imaging |
| 🎗️ | Oncology, Cancer Research |
| 🔪 | Surgery, Robotic Surgery |
| 🩺 | General Medicine, Internal Medicine |
| ❤️ | Cardiology, Cardiovascular |
| 🧠 | Neurology, Neuroscience |
| 🦠 | Microbiology, Infectious Disease |
| ⚗️ | Biochemistry, Clinical Chemistry |
| 💊 | Pharmacology, Drug Discovery |
| 🧬 | Genomics, Bioinformatics, Precision Medicine |
| 🧴 | Dermatology |
| 👶 | Pediatrics, Neonatology |
| 👁️ | Ophthalmology, Retinal Imaging |
| 🦴 | Orthopedics, Musculoskeletal |
| 🧩 | Psychiatry, Mental Health |
| 🤰 | Obstetrics & Gynecology |
| 🚑 | Emergency Medicine, Critical Care |
| 🌍 | Public Health, Epidemiology |
| 📱 | Digital Health, Telemedicine |
| 🤖 | AI & Technology |

---

## 📊 Data Sources

### Top AI News (11 sources)
OpenAI Blog · Anthropic Research · Google AI · DeepMind · Hugging Face · MIT Technology Review · VentureBeat AI · The Verge AI · Ars Technica · NVIDIA AI · Microsoft Research

### AI in Healthcare (10 sources)
Healthcare IT News · STAT News · Fierce Healthcare · Fierce Biotech · MobiHealthNews · Digital Health Today · Health Data Management · The Medical Futurist · Google Health · Microsoft Health

### Pathology & Lab Medicine (7 sources)
The Pathologist · CAP Today · Lab Manager · Dark Daily · PathologyOutlines · 360Dx · GenomeWeb

### Research Papers & Journals (18 sources)
arXiv (AI, CV, ML, q-bio, Image Processing) · bioRxiv · medRxiv · PubMed (AI in Pathology, Healthcare, Digital Pathology, Lab Medicine AI) · Nature Digital Medicine · Nature Medicine · Nature Biotechnology · The Lancet Digital Health · NEJM AI · JAMA Network Open · Journal of Pathology Informatics · Modern Pathology · AJCP · Clinical Chemistry · JCLA · Diagnostic Pathology · BMC Medical Informatics

### Open Source (3 sources)
Papers With Code · GitHub Trending · Hugging Face Papers

> See [recommended-sources.md](./recommended-sources.md) for the complete list with descriptions.

---

## 🚀 Quick Start

### Requirements

- Node.js >= 18.0.0
- pnpm (recommended) or npm

### Install & Run

```bash
# Clone the project
git clone https://github.com/SuYxh/ai-news-aggregator.git
cd ai-news-aggregator

# Install dependencies
pnpm install

# Fetch data
pnpm fetch

# Start the web UI
cd web && pnpm install && pnpm dev
```

### Commands

```bash
# Full fetch (all data sources)
pnpm fetch

# Fetch only OPML RSS feeds
pnpm fetch:opml

# Limit to first N RSS feeds (for testing)
pnpm fetch:opml ./feeds/follow.opml 10

# Web development mode
cd web && pnpm dev

# Production build
cd web && pnpm build
```

### CLI Options

| Option | Default | Description |
|:-------|:--------|:------------|
| `--output-dir` | `data` | Output directory |
| `--window-hours` | `24` | Time window in hours |
| `--archive-days` | `45` | Archive retention in days |
| `--translate-max-new` | `80` | Max translations per run |
| `--rss-opml` | `./feeds/follow.opml` | OPML feed file path |
| `--rss-max-feeds` | `0` | Max RSS feeds (0 = all) |

---

## 📁 Output Files

Generated in the `data/` directory after each run:

| File | Description |
|:-----|:------------|
| `latest-24h.json` | Last 24 hours of news |
| `latest-7d.json` | Last 7 days of news |
| `archive.json` | Historical archive (45 days) |
| `source-status.json` | Source fetch status |
| `opml-feeds.json` | OPML feed list |

---

## 🏗️ Project Structure

```
ai-news-aggregator/
├── src/                      # Data fetching engine
│   ├── index.ts              # Main entry point
│   ├── config.ts             # Configuration & keywords
│   ├── types.ts              # TypeScript types
│   ├── fetchers/             # Platform-specific fetchers
│   ├── filters/              # AI-relevance & dedup filters
│   ├── translate/            # Translation module
│   └── utils/                # Utilities
├── web/                      # React frontend
│   ├── src/
│   │   ├── components/       # UI Components
│   │   │   ├── FilterBar.tsx
│   │   │   ├── SpecialtyFilter.tsx  # Healthcare tag filter
│   │   │   ├── NewsCard.tsx         # Card with specialty badges
│   │   │   └── ...
│   │   ├── hooks/            # Custom hooks
│   │   │   └── useNewsData.ts       # Data + filtering logic
│   │   ├── utils/
│   │   │   └── healthcareTags.ts    # 21 specialty definitions
│   │   └── App.tsx
│   └── vite.config.ts
├── feeds/
│   └── follow.opml           # RSS feed subscriptions
├── recommended-sources.md    # Data source documentation
├── data/                     # Output data
└── .github/workflows/        # GitHub Actions
```

---

## 🛠️ Tech Stack

### Data Engine

| Technology | Purpose |
|:-----------|:--------|
| **TypeScript** | Type safety |
| **Cheerio** | HTML parsing |
| **rss-parser** | RSS feed parsing |
| **fast-xml-parser** | XML parsing |
| **dayjs** | Date handling |
| **p-limit** | Concurrency control |

### Web Frontend

| Technology | Purpose |
|:-----------|:--------|
| **React 18** | UI framework |
| **TypeScript** | Type safety |
| **Vite** | Build tool |
| **Tailwind CSS** | Styling |
| **Lucide React** | Icons |

---

## ✍️ Author

**Dr. Atul Tiwari**
- 📧 [atultiwari.in@gmail.com](mailto:atultiwari.in@gmail.com)
- 🌐 [https://atultiwari.in](https://atultiwari.in)

---

## 🙏 Credits

Adapted from the [AI News Aggregator](https://github.com/SuYxh/ai-news-aggregator) by **[SuYxh](https://github.com/SuYxh)**. The original project is a multi-source AI news aggregator with Chinese-language support. This fork re-focuses it on **AI in Healthcare, Pathology, and Laboratory Medicine** with English-language UI, healthcare specialty tagging, and curated medical/scientific data sources.

---

## 📝 Changelog

See [CHANGELOG.md](./CHANGELOG.md) for version history.

---

## 📄 License

MIT

---

<div align="center">

**⭐ Star this repo if you find it useful!**

[🐛 Report Issues](https://github.com/SuYxh/ai-news-aggregator/issues) · [💡 Feature Requests](https://github.com/SuYxh/ai-news-aggregator/issues)

</div>
