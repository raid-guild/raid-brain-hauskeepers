# DAOhaus Discord Cleanup

## Current Channels

### MOD ONLY

- `#collabland-join`
- `#gatehaus`
- `#collabland-config`
- `#sobol-bot-log`
- `#anti-spam`

### Welcome

- `#welcome`
- `#haus-roles`
- `#announcements`

### Public Square

- `#memes`
- `#tavern`
- `#hackathon`
- `#support`
- `#news-flash`
- `#rage-beats`
- `#bright-ideas`
- `open voice`: `speak-ez`

### PublicHaus

- `#publichaus-info`
- `#publichaus-chat`
- `public forum`: `public-forum`
- `Public HAUS Updates`
- `#pubkeepers`
- `open voice`: `open-haus`

### Protocol

- `#protocol-info`
- `#protocol-chat`
- `#projects`
- `#bug-reports`
- `#rage-ships`
- `open voice`: `protocol-voice`

### Products

- `#product-chat`
- `#products`
- `#product-activity`
- `open voice`: `product-voice`

## Current Surface Notes

- There are several overlapping general discussion channels: `#tavern`, `#bright-ideas`, `#protocol-chat`, `#product-chat`, and `#publichaus-chat`.
- Support and bug reporting are split between `#support` and `#bug-reports` (now `#change-requests`).
- Activity/reporting surfaces are split between `#news-flash`, `#rage-beats`, `#rage-ships`, `#product-activity`, and `Public HAUS Updates`.
- Voice channels exist in Public Square, PublicHaus, Protocol, and Products.
- `#projects`, `#products`, and `#hackathon` may overlap unless they have distinct current uses.

## Proposed New Structure

### Summary Of Work Completed

The Discord cleanup has been largely completed. The server guide, welcome flow, and
Protocol info surfaces have been rewritten; mod-only channels and community
onboarding have been cleaned up; and `#rage-ships` webhooks now trigger from the
canonical repos.

The updated server shape is centered on a smaller set of active channels and
roles:

- [x] edit server guide
- [x] mod channel cleanup
- [x] rewrite welcome
- [x] rewrite Protocol-info
- [x] update #rage-ships webhooks now triggering off canonical repos
- [x] cleanout community onboarding
- [x] define support flow
  - `#support` remains the public channel for questions and bug reports
  - Prism bot screens intake and moves confirmed reports into view-only
    `#bug-reports` (now `#change-requests`)
  - CR intake is locked to the new `hauskeeper` role

**New active roles**

- basic visitor
- warcamp (admin)
- hauskeeper

### Current Status

The cleanup is ready for the raid workstream to absorb the remaining support
automation decisions. Channel consolidation and role cleanup are complete enough
to operate from the proposed structure below. The remaining work is mostly
coordination and launch communication.

### Open Action Items

- [ ] Implement the support flow as part of the AI maintenance workstream.
- [ ] Create and publish an announcement post when the raid is shipped.

**Channels**

### MOD ONLY

- `#gatehaus`

### Public Square

- `#welcome`
- `#announcements`
- `#support`

### PublicHaus

- `public forum`: `public-forum`

### Protocol

- `#protocol-info`
- `#protocol-chat`
- `#bug-reports` ->> `#change-requests`
- `#rage-ships`
- `open voice`: `protocol-voice`

---
