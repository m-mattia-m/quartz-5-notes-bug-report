---
publish: true
title: 💎 Obsidian
created: 2026-01-28T20:05:03.000+01:00
modified: 2026-03-15T20:44:08.091+01:00
tags:
  - NoteTaking/Obsidian
  - Tools
---

I just started using Obsidian a few days ago (October 2025). I’ve been writing in #NoteTaking for quite a while since I used it for many documentations, school summaries, and similar projects. What I really like about Obsidian is that it’s open-source and offers a great graph view for linking notes.

The main reason I started using Obsidian is that I want to build my own knowledge base system, which I previously managed in Notion. I’m still happy with Notion, but for documentation, I prefer being able to easily link pages and visualize connections between topics in a graph view. This makes it much easier to find and explore related content.

To make my notes accessible to others, I also started using [[Quartz|Quartz]] to publish them publicly.

# [[Security]]

- [[E2E-Encryption]] Can be verified with [this article](https://obsidian.md/blog/verify-obsidian-sync-encryption/).
- [How does obsidian work](https://kristofa.eu/2024-06-01-basic-readonly-sharing-obsidian-notes/)

# Obsidian API

> Obsidian follows the local-first approach and therefore it doesn't have a own REST API.

[obsidian-local-rest-api](https://github.com/coddingtonbear/obsidian-local-rest-api) is a tool which add a REST API to your local Obsidian instance.

# Clients

- [Obsidian](https://obsidian.md)
- [Headless-Sync](https://github.com/obsidianmd/obsidian-headless)
  - [[Obsidian Headless Client]]
- [CLI](https://obsidian.md/cli)
- [Browsidian](https://github.com/blamouche/browsidian)
  - [Browsidian: my web editor for Obsidian](https://lamouche.fr/notebook/posts/browsidian-my-web-editor-for-obsidian/)

## Obsidian Like [[Visual Studio Code]]

- [Foam](https://github.com/foambubble/foam)
- [Dendron](https://github.com/dendronhq/dendron)

# Updated files of an Obsidian Vault

## add-frontmatter-tag.sh

```bash
#!/usr/bin/env bash

set -euo pipefail

DIR="${1:-}"

if [[ -z "$DIR" || ! -d "$DIR" ]]; then
  echo "Usage: $0 <directory>"
  exit 1
fi

for file in "$DIR"/*; do
  [[ -f "$file" ]] || continue

  # Must start with frontmatter
  if ! head -n 1 "$file" | grep -q '^---'; then
    continue
  fi

  # Skip if Entertainment already present
  if awk '
    /^---$/ && ++d == 2 { exit }
    /^[[:space:]]*-[[:space:]]*Entertainment$/ { found=1 }
    END { exit found ? 0 : 1 }
  ' "$file"; then
    continue
  fi

  awk '
    BEGIN {
      in_frontmatter = 0
      tags_found = 0
      inserted = 0
    }

    /^---$/ {
      in_frontmatter++
      if (in_frontmatter == 2 && !tags_found && !inserted) {
        print "tags:"
        print "  - Entertainment"
        inserted = 1
      }
      print
      next
    }

    in_frontmatter == 1 && /^tags:/ {
      tags_found = 1
      print
      print "  - Entertainment"
      inserted = 1
      next
    }

    { print }
  ' "$file" > "${file}.tmp"

  mv "${file}.tmp" "$file"
  echo "Updated: $file"
done
```
