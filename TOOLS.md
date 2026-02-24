# TOOLS.md - Local Notes

## Development Rules

### Network URLs
**Rule:** Always provide network-accessible URLs when running local dev servers.

**How to find the URL:**
1. Check dev server output for "Network:" line
2. Example: `Network: http://192.168.2.26:3000`
3. Format: `http://192.168.XX.XX:3000`

**Usage:**
- Run `npm run dev` or similar
- Look for "Local:" and "Network:" URLs in output
- Provide the "Network:" URL for device testing

---

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.
