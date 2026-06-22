# OnCue MVP UX Architecture

**Version:** 3.0
**Date:** June 21, 2026
**Phase:** Pre-implementation — architecture only. No Lovable build has begun.
**Scope:** MVP required for initial validation on real weddings.

---

## Document Status

**Where this document lives:** Repository only — `docs/architecture/mvp-ux-architecture.md`

**Google Drive integration:** The founder has confirmed (Section 9, item D) that the confirmed content of this document must be merged into the authoritative Master Google Docs (`OnCue Master Document V2.gdoc` and `OnCue Founder Decisions Log.gdoc`) before Lovable implementation begins. The Master Docs remain the authoritative source of product strategy. This document is the working implementation specification and must not diverge from them.

**Source documents used to write this:**
- `OnCue_Master_Strategy_and_Brand_Guardrails.md`
- `OnCue_Product_Architecture_and_Technical_Guardrails.docx`
- `OnCue_MVP_Specification_and_Roadmap.docx`
- `docs/FOUNDER_DECISIONS.md`
- Eleven explicit founder decisions applied in Version 2.0 (June 21, 2026)
- Ten red-team additions applied in Version 3.0 (June 21, 2026): Review Required workflow, Event Readiness Checklist, comprehensive rollback, Google Drive merge confirmed, What's Changed Since Last Visit, vendor status tracking, emergency contact layer, mobile-first one-handed design rule, required PDF emergency backup, strengthened smart defaults

**All items in Section 9 are now confirmed. No open questions remain before Lovable implementation.**

---

## Revision History

| Version | Date | What changed |
|---|---|---|
| 1.0 | June 21, 2026 | Initial draft from Master Docs |
| 2.0 | June 21, 2026 | Applied 11 founder decisions: questionnaire model, family group scope, couple auth, vendor marketing, Wedding Day Mode delay-first design, planner roles, couple PDF, QR codes, pre-fill deferral, custom branding deferral, location sharing plan |
| 3.0 | June 21, 2026 | Applied 10 red-team additions: Review Required workflow (not formal approval queue); Event Readiness Checklist (7 items, not binary); comprehensive MVP rollback (undo/redo + automatic snapshots + full timeline restore + change log + version comparison); Google Drive merge confirmed; What's Changed Since Last Visit; vendor status tracking (Invited / Viewed / Confirmed); emergency contact layer; mobile-first one-handed as hard design rule; PDF backup required (not optional); smart defaults required for every field. All Section 9 items confirmed. |

---

## Design Principles

These principles govern every screen, every interaction, and every default.

**1. Mobile-first, one-handed.** Every screen is designed for a photographer holding a phone in one hand during a wedding. Touch targets must be large, tap paths must be short, and no critical action requires two hands or precise fine-motor control. Desktop is a planning tool. Mobile is the execution tool.

**2. Smart defaults over configuration.** Every field must have a sensible default. A photographer who fills in nothing beyond event date and couple names must still get a usable baseline timeline. Defaults come from the template; they are overridable, not mandatory.

**3. PDF as required emergency backup.** The printed timeline is not a convenience feature — it is the safety net for the wedding day. OnCue must ensure a PDF backup exists before the event date, and must warn clearly if one has not been downloaded.

**4. Clarity over completeness.** When in doubt, show less. Surface what matters for the current moment. Planning Mode can show more; Execution Mode must show less.

---

## 1. Core User Journeys

### Role Mapping

| Role | Who | Access model |
|---|---|---|
| **Owner** | Photographer (Phase 1 primary user). Creates the OnCue account and owns the event. | Full account |
| **Planner** | Wedding planner invited as a collaborator or co-owner. | Full account (invited) |
| **Vendor** | DJ, videographer, florist, hair/makeup, officiant, and other service providers. | No account — shareable link only |
| **Client / Couple** | The couple being married. | Lightweight account (magic link or Google sign-in) |

---

### Journey 1: Owner (Photographer)

**Who:** The photographer who created the OnCue account.

#### A. Create and set up a new event

**Trigger:** Photographer books a wedding.

**Desired outcome:** A dependency-aware draft timeline is populated from the wedding template with smart defaults. The questionnaire has been started. The couple has been invited.

**Key screens:**
1. Dashboard → Create Event
2. Template selection (Wedding)
3. Event details (date, couple names, primary location)
4. Timeline Editor — template pre-populated with smart defaults
5. Questionnaire — owner begins filling during or after the booking consultation
6. Invite couple — sends a magic link or Google sign-in invitation

---

#### B. Build and refine the timeline

**Trigger:** Questionnaire data is sufficient to translate into a working timeline.

**Desired outcome:** A constraint-aware timeline with anchors, travel blocks, family groups, and durations that can survive change.

**Key screens:**
1. Timeline Editor — add, reorder, and time activities
2. Activity Detail Panel — set duration, anchor type, location, priority, visibility, dependencies
3. Group Photo Optimizer — generate and sequence family and wedding party groups
4. Vendor Role view preview — confirm what each vendor will see

---

#### C. Collaborate and publish

**Trigger:** Timeline is ready for planner or couple review.

**Desired outcome:** Couple and planner have viewed the timeline. PDF backup is downloaded. Event Readiness Checklist shows all items complete. Event is ready to execute.

**Key screens:**
1. Timeline Editor — publish / share
2. Change Review — review all couple proposals; see collaborator changes applied under Review Required
3. PDF Export — download compact and filtered versions (required before event date)
4. Event Readiness Checklist — confirm each readiness item is met

---

#### D. Execute on wedding day

**Trigger:** Wedding day.

**Desired outcome:** Photographer navigates the day with complete clarity. When anything runs late, the system shows the impact and offers recovery options immediately.

**Key screens:**
1. Wedding Day Mode — compact execution view
2. Delay adjustment panel — enter delay, see impact, select recovery, choose who to notify
3. Emergency contacts — accessible in one tap from the main view

---

### Journey 2: Planner (Collaborator or Co-owner)

**Who:** A wedding planner invited to the event.

**Trigger:** Photographer invites the planner as a collaborator or co-owner.

**Desired outcome:** Planner can co-manage the timeline and coordinate vendors without owning the photographer's account.

**Key screens:**
1. Invitation email → account sign-in or creation
2. What's Changed Since Last Visit — summary of changes since the planner last accessed the event
3. Timeline Editor — full editing access
4. Questionnaire — can view and edit; collaborator edits apply immediately under Review Required (owner is notified and can revert); co-owner edits apply directly
5. Change Review — review couple proposals; co-owner can approve; collaborator can view but not approve
6. Vendor Role management — configure visibility, track vendor status, generate vendor links
7. Wedding Day Mode — execution view identical to owner's
8. PDF Export — all formats

**Distinction from Owner:**
- Cannot delete the event
- Cannot manage account billing
- Collaborator: edits apply immediately; owner is notified via Review Required; owner can revert in the change log
- Co-owner: full event authority; can approve couple proposals; cannot access account settings

---

### Journey 3: Vendor (Team Member)

**Who:** A DJ, videographer, florist, hair/makeup artist, officiant, or any other service provider.

**Trigger:** Owner or planner generates and shares a vendor-specific link. No OnCue account required.

**Desired outcome:** Vendor sees only the activities relevant to their role and can print a one-page reference for the day.

**Key screens:**
1. Vendor link landing — no login required. Lightweight marketing prompt: "Running your own events? Try OnCue free." Vendor can dismiss or claim their free vendor profile. One-tap confirmation: "I've got it" updates vendor status to Confirmed.
2. Vendor-Filtered Timeline — read-only view of only their relevant activities
3. PDF Export — one-page filtered view for their role

**Vendor status tracking:** Each vendor link has a status visible to the owner and planner:
- **Invited** — link generated and shared; vendor has not yet opened it
- **Viewed** — vendor has opened the link at least once
- **Confirmed** — vendor has tapped "I've got it" on the vendor link landing (explicit confirmation)

**Vendor sees:**
- Activity title, start time, duration
- Location
- Notes flagged for vendor visibility
- Their relevant setup and capture checklist items

**Vendor does not see:**
- Other vendors' activities (unless they overlap in a shared section)
- Family group detail or questionnaire data
- Internal photographer notes
- Full timeline

**Restrictions:** Read-only. No edits of any kind.

---

### Journey 4: Client / Couple (Individual User)

**Who:** The couple being married.

**Trigger:** Photographer invites the couple after booking. Couple receives a magic link or can sign in with Google.

**Authentication:** Magic email link or Google sign-in. The sign-in flow must feel lightweight and welcoming — not a professional account setup. Couple does not choose a plan, enter a credit card, or configure settings.

**Desired outcome:** Couple has completed the questionnaire, reviewed the timeline, and submitted any suggestions — all without needing to understand constraint logic.

**Key screens:**
1. Welcome / sign-in — magic link from email or Google sign-in; lands directly in their event
2. What's Changed Since Last Visit — plain-language summary shown when returning after changes have been made (e.g., "Your suggestion to start portraits at 5:30pm was approved.")
3. Questionnaire — their sections of the shared questionnaire; can complete and return to update
4. Timeline Review — simplified read-only view of the timeline
5. Suggest a Change — inline on any activity; does not modify the live timeline; goes to owner review
6. Suggestion status — couple can see whether their suggestions are pending, approved, or declined

**What the couple can edit:**
- The questionnaire (their sections) — changes are proposals requiring owner approval
- Suggest timeline changes — proposed changes only
- Family/group photo participants — proposed changes only

**What the couple cannot do:**
- Directly edit or reorder any timeline activity
- View internal photographer notes
- See other vendors' contact information
- Access the full constraint/optimization editor

**Note on couple changes:** All couple changes — to questionnaire answers, suggested timeline edits, family group members, vendor contacts, or key event details — require owner or co-owner approval before being applied to the live event.

---

## 2. Product Modes

### Planning Mode

**Purpose:** Build, refine, and collaborate on the timeline before the wedding day. Detail-rich. Full editor.

**Available actions:**
- Create and configure the event
- Complete or update any part of the questionnaire
- Edit timeline activities: title, duration, location, anchor type, priority, visibility, dependencies, notes
- Drag and reorder activities (dependency chain updates accordingly)
- Undo / redo any change in the current session
- View automatic snapshots (taken at key milestones); restore or compare to a prior version
- View the change log and version comparison summary
- Run the Group Photo Optimizer (family and wedding party groups)
- Invite planner, couple, and generate vendor links
- Review couple proposals and approve or decline
- Review collaborator changes flagged under Review Required; revert if needed
- Export PDF in any available format
- Preview any role-filtered view

**Data displayed:**
- Full timeline with all activities and sections
- Durations, calculated start/end times, buffers, anchor indicators
- Location assignments and travel blocks
- Constraint warnings and dependency chain impacts
- Group photo list with estimated durations and total block time
- Pending couple proposals (badge count)
- Review Required notifications (collaborator changes awaiting owner awareness)
- Change log, version history, and snapshot list
- Event Readiness Checklist

**Event Readiness Checklist:**

An event is ready for the wedding day when all of the following are met. Each item shows a checkmark when satisfied and a prompt when not.

| # | Readiness item | How it is met |
|---|---|---|
| 1 | Questionnaire is complete | All required questionnaire sections have been filled in |
| 2 | Group photos are sequenced | Group Photo Optimizer has been run and sequence confirmed |
| 3 | PDF backup downloaded | At least one compact or full PDF has been downloaded |
| 4 | No critical constraint warnings | No unresolved anchor threats, chain violations, or duration compressions |
| 5 | All couple proposals resolved | No pending couple proposals awaiting owner decision |
| 6 | At least one vendor link shared | At least one vendor has been sent their filtered link |
| 7 | Emergency contacts entered | At least one emergency contact is recorded in the questionnaire |

The checklist is visible in Planning Mode and as a summary card on the Dashboard event card near the event date. The system warns clearly if the event date is within 7 days and the checklist is not complete.

**When Planning Mode is unavailable:**
After the event date passes, the event is archived and becomes read-only. Planning Mode is locked. The timeline and questionnaire can be viewed and exported but not edited.

---

### Execution Mode (Wedding Day Mode)

**Purpose:** Navigate the wedding day with maximum clarity and minimum cognitive load. Execute, not plan.

**Primary feature: Running late / delay adjustment.**
The central day-of action is not marking activities complete. It is handling delays. The system must make it fast and easy to say "we are running X minutes behind" and immediately understand the impact and recovery options.

**Available actions:**
- View the current activity and what is coming next
- See who is responsible for the current activity
- Tap "Running Late" — enter delay in minutes, see which activities are impacted, select a recovery option, choose who to notify
- Accept or reject a suggested recovery change (change only applies after approval)
- Mark an activity complete (available, but the system does not rely on this — wedding days are too busy)
- Open the full timeline reference (read-only)
- Access the pre-downloaded PDF backup (offline-safe)
- Access emergency contacts — one tap from the main view

**Delay adjustment flow:**
1. Tap "Running Late"
2. Enter delay amount (quick options: 5, 10, 15, 20, 30+ minutes)
3. System shows: which upcoming activities are affected, which anchors are threatened, what the cascade looks like
4. System presents recovery options with the likely impact of each
5. Owner or co-owner selects a recovery option
6. System asks: who should be notified? (suggests only people whose activities are meaningfully affected)
7. Owner confirms notifications
8. Timeline updates; notifications sent to confirmed recipients only

**The system does not automatically notify anyone.** Notifications require explicit human approval, and only affected parties are ever suggested.

**Data displayed:**
- NOW: current activity title, location, assigned people, elapsed and remaining time
- NEXT: 2–3 upcoming activities (title, time, location)
- Attention flag: visible when a delay, constraint warning, or missing-person issue exists
- Recovery options panel (opens when delay is flagged)
- Emergency contacts (accessible in one tap from the main view; always visible)

**What Execution Mode is not:**
- Not a drag-and-drop editor
- Not a place to restructure the timeline
- Not a group photo optimizer
- Not a full questionnaire

---

### Mode Transitions

| Transition | Trigger | Who |
|---|---|---|
| Planning → Execution | Manual switch, or system prompt on event date | Owner, Co-owner planner |
| Execution → full timeline reference | "View full timeline" link inside Wedding Day Mode | Owner, Co-owner planner |
| Execution → Planning edit | Not available on event day | — |
| Event → Archived | Automatic when event date passes | System |

---

## 3. Page Map / Navigation

### Global Navigation (Signed-in Professional)

```
Dashboard             ← event list; primary landing page after sign-in
  └── Create Event
Account / Settings    ← plan, profile
```

### Per-Event Navigation

```
Event: [Name]
  ├── Timeline          ← Planning Mode editor (default)
  ├── Questionnaire     ← shared event questionnaire
  ├── Group Photos      ← Group Photo Optimizer (family + wedding party)
  ├── Vendors           ← role assignments, vendor status tracking, link generation
  ├── Wedding Day       ← Execution Mode (becomes prominent near event date)
  └── Export            ← PDF: compact, full, vendor-filtered, group-photo-only
```

**What's Changed Since Last Visit** appears as a dismissable banner or card when a user returns to an event where changes have been made since their last visit. It lists the most recent changes in plain language. Shown to: owner, planner, and couple. Dismissed by the user or automatically after 24 hours.

### Change Review (global, not per-tab)

Pending couple proposals appear as a persistent badge across the event. Change Review is accessible from any tab, not buried in one section.

**Review Required notifications** (for collaborator changes already applied) appear as a separate indicator. The owner reviews these in the change log and can revert if needed.

### Client / Couple Navigation (after sign-in)

```
[Event Name] — Your Timeline
  ├── Questionnaire     ← their sections of the shared questionnaire
  ├── Timeline          ← simplified read-only view with suggest-a-change per activity
  └── Suggestions       ← status of submitted suggestions (pending / approved / declined)
```

What's Changed Since Last Visit is shown when the couple returns and something has changed (e.g., a suggestion was approved, the timeline was updated).

### Vendor View (no sign-in)

```
Vendor Link Landing
  ├── [Role]-Filtered Timeline   ← read-only, their activities only
  ├── PDF Download               ← their filtered view
  ├── "I've got it" confirmation ← one-tap; updates status to Confirmed
  └── Marketing prompt           ← "Running your own events? Try OnCue free." (dismissable)
```

### Mobile Design Rules

**One-handed operation is a hard requirement, not a guideline.**

Every action a photographer must take during the wedding day must be completable with one thumb on a phone in portrait mode. Specifically:

- Touch targets minimum 44×44pt
- Primary action always in the bottom half of the screen
- Critical actions (Running Late, delay amount, recovery selection) reachable in two taps maximum from the main Wedding Day screen
- No action requiring simultaneous multi-touch for core workflows
- Swipe-to-dismiss is supplemental; tap is always the primary path
- Planning Mode on mobile collapses to a bottom tab bar; timeline list is scrollable; detail panel opens as a bottom sheet
- All PDF exports must be portrait-oriented and legible when printed from a phone browser
- Couple's interface must feel native on a smartphone — they will not use a laptop

### Desktop Considerations

- Planning Mode uses a two-panel layout: timeline list left, detail/edit panel right.
- Group Photo Optimizer benefits from a two-panel layout: group list left, people picker right.
- Questionnaire is a single-column scrollable form on all screen sizes.
- Wedding Day Mode on desktop mirrors the mobile card layout. It is used at events, not at desks.

---

## 4. Key Screens and Content Hierarchy

### Screen 1: Dashboard — Event List

**Purpose:** Entry point for the professional user. Show all events and their status.

**Primary action:** Create a new event.

**Secondary actions:** Open an existing event; view archived events.

**Information hierarchy:**
1. Upcoming events sorted by date (ascending)
2. Each card: wedding name, date, couple names, status badge (Draft / Active / Day-of / Archived), days-until indicator, pending proposals badge, vendor status summary (X of Y confirmed), Event Readiness Checklist summary (near event date)
3. Archived events (collapsed)
4. Plan status (events remaining on free tier, or current plan)

**Success metric:** Owner finds and opens any event in one tap.

---

### Screen 2: Create Event

**Purpose:** Start a new event record.

**Primary action:** Confirm details and open the Timeline Editor.

**Secondary actions:** Change template.

**Information hierarchy:**
1. Template selector (Wedding is the only MVP template)
2. Event date
3. Couple names
4. Primary location (optional; can be set later)
5. Create

**Smart defaults on creation:** The wedding template pre-populates a complete baseline sequence with default durations, anchor types, visibility settings, and location placeholders. The owner can begin working immediately without configuring anything. All defaults are labeled and overridable.

**Success metric:** Event opens in Timeline Editor with the wedding template pre-populated within 3 seconds.

---

### Screen 3: Questionnaire

**Purpose:** One shared event questionnaire. The owner may begin during a consultation. The couple completes and updates it over time. Any edits made by a non-owner are proposals requiring owner approval.

**Primary action:** Complete or update a section.

**Secondary actions:** Invite couple to complete their sections; view pending questionnaire proposals.

**Questionnaire sections:**

1. **Core event details** — couple names, preferred surname, date, phone numbers, email addresses
2. **Locations** — getting ready (bride side), getting ready (groom side), first look, ceremony, portraits, reception, sunset portrait location
3. **Group photo participants** — all people needed for family or wedding party photos. Not limited to immediate family. Includes: parents, step-parents, grandparents, siblings, children, extended family, chosen family, VIPs, close relatives, anyone the couple wants in a group photo. Each person: name, relationship, notes (elderly, mobility needs, arriving late, etc.)
4. **Wedding party** — best man, MOH, bridesmaids, groomsmen, flower girl, ring bearer, MC, officiant; people who may appear across multiple group configurations
5. **Vendors** — planner, venue, florist, catering, DJ, hair/makeup, videographer, cake, decor; each with name, contact, and arrival time
6. **Preferences** — ideal portrait location, dream space, important people and moments, emotional priorities
7. **Priorities** — which moments matter most; which moments are most flexible if time or weather changes
8. **Emergency contacts** — people to call if something goes wrong on the wedding day. Not limited to the couple. Includes: planner's personal mobile, venue coordinator, family point-of-contact, any on-call vendor contact. Each entry: name, role, phone number. Required for Event Readiness Checklist item 7. Accessible in one tap from Wedding Day Mode.

**Approval behavior:** If the couple or a collaborator edits a questionnaire field, that change is submitted as a proposal. The owner sees a "Questionnaire proposals pending" indicator. Approved changes are applied; declined changes are preserved in the log.

**Success metric:** Enough data is collected from the questionnaire to auto-populate location inheritance, travel blocks, and group photo suggestions without manual entry.

---

### Screen 4: Timeline Editor (Planning Mode)

**Purpose:** The primary working canvas. Build, sequence, and configure the dependency-aware timeline.

**Primary action:** Add, edit, or reorder activities.

**Secondary actions:** Set anchor type; override location; adjust buffer or minimum duration; preview a role-filtered view; undo / redo; publish or share.

**Information hierarchy:**
1. Timeline list — ordered with inline start times, durations, location labels, anchor indicators
2. Section dividers (Getting Ready, First Look, Ceremony, Portraits, Reception, etc.)
3. Travel blocks — inserted automatically between location changes
4. Constraint warnings — shown inline when an anchor is threatened, a duration is compressed, or a dependency chain is affected
5. Activity detail panel — opens on selection; shows all fields
6. Toolbar — add activity, undo, redo, preview view, pending proposals count, Review Required badge, publish/share

**Success metric:** Owner can move an activity and immediately see which downstream activities shifted, which anchors held, and whether any minimum durations were violated — without leaving this screen.

---

### Screen 5: Activity Detail / Edit Panel

**Purpose:** View and configure all fields for one activity.

**Primary action:** Save changes.

**Secondary actions:** Delete activity; duplicate activity; set dependency.

**Information hierarchy:**
1. Title
2. Duration / minimum duration
3. Location (inherited or overridden; shows parent location when inherited)
4. Anchor type: Locked / Preferred / Flexible / Movable with approval
5. Priority: Critical / Important / Flexible / Optional / Buffer
6. Visibility: which roles can see this activity (Owner, Planner, Couple, specific vendor roles)
7. Dependencies: before/after relationships
8. Requires people: names or roles who must be present
9. Weather sensitive: toggle + outdoor/indoor note
10. Internal notes (owner-only; not visible to couple or vendors)
11. Vendor-facing notes (visible to vendors with access to this activity)
12. Checklist items: setup, capture, recovery

**Success metric:** All constraint fields reachable without scrolling past the fold on a tablet.

---

### Screen 6: Group Photo Optimizer

**Purpose:** Generate, sequence, and configure group photo combinations for both family photos and wedding party photos, based on questionnaire participants.

**Primary action:** Accept or adjust the auto-generated sequence.

**Secondary actions:** Add a group; remove a group; reorder groups; add or remove people from a group; set estimated duration per group; export to timeline.

**Information hierarchy:**
1. Auto-generated group list — default sequencing prioritizes getting through largest groups first, then prioritizing elderly and children early (so they can be released)
2. Each group card: group name, required people, estimated duration, status (scheduled / completed / deferred / missed)
3. Cross-group people indicator: shows when a person appears in multiple groups (prevents releasing them too early)
4. Missed person workflow: move group to end, defer to recovery queue, or note for later
5. Total estimated block duration — updates live as groups are adjusted
6. Export to timeline block or as separate family-photo PDF

**Note:** This optimizer covers both family group photos and wedding party combinations. Anyone added in Section 3 of the questionnaire (group photo participants) and Section 4 (wedding party) can appear here.

**Success metric:** Photographer reviews and confirms the group sequence in under five minutes from questionnaire data.

---

### Screen 7: Vendor Role Management

**Purpose:** Configure what each vendor role can see. Generate and share vendor access links. Track vendor status.

**Primary action:** Generate a vendor access link for a specific role.

**Secondary actions:** Configure role visibility settings; revoke or regenerate a link; preview the vendor's view; copy link.

**Information hierarchy:**
1. Role list (Planner, DJ, Videographer, Florist, Hair/Makeup, Venue, Officiant, Custom)
2. Per role: assigned activities, visibility scope, vendor status (Invited / Viewed / Confirmed)
3. Copy link button (QR code is optional and lower priority)
4. Preview vendor view

**Vendor status definitions:**
- **Invited** — link generated and shared; vendor has not yet opened it
- **Viewed** — vendor has opened the link at least once (tracked by link access)
- **Confirmed** — vendor has tapped "I've got it" on the vendor link landing (explicit confirmation)

**Vendor link landing behavior:** When a vendor opens their link, they see their filtered timeline. A lightweight marketing prompt is shown: "Planning your own events? Try OnCue free." The vendor can claim a free vendor profile or dismiss. No account is required to view their timeline.

**Success metric:** Owner generates a DJ-specific link in under 30 seconds and can see at a glance which vendors have confirmed receipt.

---

### Screen 8: Review Required / Change Review

**Purpose:** One place to manage all proposed changes and collaborator activity. Couple proposals require explicit approval before being applied. Collaborator changes (Review Required) have already been applied; owner reviews and can revert.

**Two distinct workflows:**

**Workflow A — Couple proposals (require approval):**
- Primary action: Approve or reject a proposed change.
- Secondary actions: Edit a proposed change before approving; leave an internal note; batch-approve multiple proposals.
- Applies to: all couple changes (timeline suggestions, questionnaire updates, group photo participant additions, vendor contact updates)
- Change is NOT applied until the owner or co-owner explicitly approves.

**Workflow B — Collaborator Review Required (already applied):**
- Primary action: Review the change log entry.
- Secondary actions: Revert a change; leave an internal note.
- Applies to: collaborator timeline edits and questionnaire updates made under Review Required
- Change is already live. Owner reviews it and can revert if needed. No approval action is required.

**Information hierarchy:**
1. Pending couple proposals — most recent first; badge count visible across the event
2. Each proposal: change type, original value vs. proposed value, submitted by, submitted at
3. Approve / Decline / Edit and Approve (for couple proposals)
4. Review Required log — collaborator changes applied since last owner visit; each entry: what changed, who changed it, when; Revert button
5. Resolved history (collapsed)

**What's Changed Since Last Visit** surfaces here as a filtered log view: all changes — approved proposals, collaborator edits, owner edits — since the viewer's last session.

**Success metric:** Owner resolves all pending couple proposals in one session; reviews collaborator changes without a blocking approval step; returns to a clean event state.

---

### Screen 9: Wedding Day Mode (Execution Mode)

**Purpose:** Navigate the wedding day with maximum clarity. The hero action is delay handling, not task completion.

**Primary action:** Handle a delay — enter how many minutes behind, see the impact, choose recovery.

**Secondary actions:** View current and upcoming activities; mark an activity complete (optional, not relied upon); open full timeline reference; access PDF backup; access emergency contacts.

**Information hierarchy (compact card layout):**
1. **NOW** — activity title, location, assigned people, time remaining
2. **NEXT** — 2–3 upcoming activities (title, time, location — minimal)
3. **Attention flag** — appears when delay, constraint warning, or missing person is detected
4. **Running Late button** — prominent, accessible from the main view; one tap to open the delay panel
5. **Emergency contacts** — accessible in one tap from the main view; always reachable without navigating away
6. Full timeline reference link — secondary prominence

**Delay panel hierarchy:**
1. "How many minutes behind are you?" — quick options: 5 / 10 / 15 / 20 / 30+ / custom
2. Impact summary: list of affected upcoming activities
3. Recovery options: 2–4 option cards, each showing what changes and the expected outcome
4. After selecting recovery: "Who should we notify?" — suggested list of only affected parties; owner can add, remove, or dismiss
5. Confirm — applies timeline change, sends notifications

**Emergency contacts panel:** Opens from the main Wedding Day Mode view. Shows name, role, and phone number for each contact entered in the questionnaire. One-tap to call. No internet connection required (data loaded when Wedding Day Mode is entered).

**Mark complete behavior:** Exists as a secondary tap action on the current activity. The system does not prompt for it, does not require it, and does not calculate event progress from it. If an activity is marked complete, it is noted in the log. The timeline advances by time, not by completion taps.

**Success metric:** On a phone, in outdoor light, with one hand, the owner can handle a 15-minute delay — see the impact, pick a recovery option, notify affected parties — in under 60 seconds.

---

### Screen 10: PDF Export

**Purpose:** Generate printable emergency backup views of the timeline. PDF is the required safety net for the wedding day — it must exist before the event begins.

**Primary action:** Download the selected view as a PDF.

**Secondary actions:** Choose export format; preview before download.

**Export formats:**
1. Compact itinerary — one-page pocketable format; day-of reference
2. Full timeline — all activities, all fields, all notes
3. Vendor-filtered — one role's relevant activities only
4. Group-photo-only — group sequence with required people and estimated durations
5. Couple's view — activities visible to couple role; available for couple to download from their interface

**PDF is a required emergency backup.** If no PDF has been downloaded before the event date, the system shows a persistent warning in Planning Mode and flags this item as incomplete in the Event Readiness Checklist. The warning does not block usage but is prominent. The export screen displays the last download date and format downloaded.

**Success metric:** Photographer downloads and prints a compact itinerary in one tap. Vendor could follow it without opening a screen. A PDF exists before the event date in every event that reaches Day-of status.

---

### Screen 11: Client / Couple View

**Purpose:** Let the couple complete the questionnaire, review the timeline, and submit suggestions — in a welcoming, simple interface that does not feel like a professional tool.

**Primary action:** Complete the questionnaire.

**Secondary actions:** Review the timeline; suggest a change; view suggestion status.

**Sign-in experience:** Magic email link (tap link in email, lands directly in the event) or Google sign-in. No plan selection, no settings, no onboarding steps. Couple lands directly in their event view.

**Information hierarchy:**
1. Welcome card — couple's names, event date, photographer's name
2. What's Changed Since Last Visit — shown when returning after changes have been made; plain-language summary (e.g., "Your suggestion to start portraits at 5:30pm was approved." or "The ceremony timeline was updated.")
3. Questionnaire — their sections only; progress indicator; returns to this screen
4. Timeline review — simplified display (time, activity, location; no internal notes, no constraint data)
5. "Suggest a change" per activity — opens a simple form; submits to owner for review
6. My suggestions — list of submitted suggestions and their current status

**Success metric:** Couple completes their questionnaire sections and reviews the full timeline without contacting the photographer for help.

---

## 5. Timeline Intelligence

### Creation Flow

1. Owner creates the event, selects the Wedding template.
2. Template pre-populates a baseline sequence with smart defaults: estimated durations per activity type, anchor types, location placeholders, visibility settings, and priority levels. No configuration required to begin working.
3. As questionnaire sections are completed, the engine fills in:
   - Location IDs from questionnaire locations
   - Travel blocks auto-inserted when the location changes between activities
   - Group Photo Optimizer seeded from questionnaire participants
   - Weather-sensitive flags applied to outdoor activities
   - Setup/service activities surfaced from selected vendors (e.g., audio setup if videographer is selected)
4. Owner reviews, adjusts, and finalizes the timeline.
5. Constraint engine evaluates the chain and surfaces warnings before the timeline is published or shared.

### Smart Defaults

Every field has a sensible default. A photographer with no prior OnCue experience must be able to use the system from the first event without configuring anything.

| Field | Default behavior |
|---|---|
| Duration | Template provides a reasonable estimate per activity type (e.g., 15 min for getting-ready detail shots, 60 min for ceremony, 90 min for portraits). Owner adjusts. |
| Anchor type | Ceremony is Locked. Getting ready start, first look, and reception start are Preferred. All other activities are Flexible by default. |
| Location | Inherited from the section's location. Overridden at the activity level when needed. |
| Priority | Critical for ceremony and first look. Important for reception start, cake cutting, first dances. Flexible for everything else. |
| Visibility | Couple sees: ceremony, key portrait blocks, reception events. Vendors see: their role-specific activities. Internal notes are owner-only by default. |
| Travel time | Default estimates by location pair (same-building: 5 min; different address: 15 min). Owner adjusts based on actual knowledge. |
| Activity order | Template sequence. Owner reorders as needed. |

All defaults are visible, labeled as defaults, and overridable. The system never silently re-applies a default after the owner has manually changed a field.

### Version History and Rollback

OnCue maintains a complete version history for every event timeline. The rollback system has four components:

**1. Undo / redo:** In-session, within the Timeline Editor. Standard undo/redo behavior. Does not persist across sessions.

**2. Automatic snapshots:** Taken at key milestones — timeline publish, PDF download, collaborator invite, first edit after opening the event, and once per hour during an active editing session. Each snapshot is labeled with a timestamp and the triggering action.

**3. Full timeline restore:** Any automatic snapshot can be restored. Restoring replaces the current timeline with the snapshot state. The owner must explicitly confirm before a restore is applied. Restoring creates a new snapshot entry in the log so the action is traceable.

**4. Change log and version comparison summary:** Every change to the timeline — by any user — is recorded in the change log. The version comparison summary shows a before/after diff between any two snapshots: what was added, removed, or modified, and by whom.

### Interaction Patterns

- **Drag to reorder:** Moving a flexible activity recalculates all downstream start times. Anchored activities do not move.
- **Extend a duration:** Downstream activities shift. If a downstream anchor is threatened, a warning appears before the change is saved.
- **Anchor types:**
  - Locked — never moves under any condition
  - Preferred — moves only with explicit owner approval
  - Flexible — moves silently within limits
  - Movable with approval — moves but requires a notification to affected parties
- **Flag a delay (Execution Mode):** Owner enters delay in minutes. Engine evaluates cascade impact and presents recovery options. Nothing changes until the owner approves.

### Constraint Warnings

| Scenario | System response |
|---|---|
| Activity extended past a downstream anchor | Warning: "Ceremony is locked at 4:00pm. Extending cocktail hour by 20 minutes will leave a 20-minute gap. Accept, compress, or adjust?" |
| Location changes without a travel block | Suggestion: "Getting ready is at Hotel A; first look is at Location B. Add a travel block? Estimated 15 minutes." |
| Group photo block shorter than estimated group total | Warning: "Your family photo groups are estimated at 45 minutes. Current block is 30 minutes. Extend the block or reduce groups?" |
| Sunset portrait scheduled after actual sunset | Suggestion: "Sunset on [date] is at 8:12pm. Sunset portraits are scheduled for 8:30pm. Move to 8:00pm?" |
| Required person has no confirmed arrival time | Warning: "Officiant is required at the ceremony but their arrival time is not set." |
| Minimum duration violated by a proposed move | Warning: "Moving this activity compresses it below its minimum duration of 10 minutes." |

### Rule-Based Intelligence (no AI required)

- Dependency chain calculations and cascading time shifts
- Anchor protection and violation detection
- Location inheritance down a section until overridden
- Travel block insertion when location changes
- Duration compression logic
- Sunset and sunrise time calculation from event date and location
- Constraint warning evaluation
- Recovery option generation from constraint rules
- Smart defaults application from template

### AI-Assisted or Heuristic Intelligence

- **Group photo sequencing (V1 heuristic):** Default sort by group size; prioritize elderly and small children early. This is a rule in V1; AI ranking improves in later versions.
- **Recovery option ranking (V1 heuristic):** Options ranked by least disruption and fewest downstream changes. AI-improved in later versions from usage patterns.
- **Questionnaire pre-fill from past events:** Deferred. Later versions may offer section-level defaults or guidance templates, but names, contacts, and specific data from past events will not be pre-filled.

### Planning vs. Execution Behavior

| Behavior | Planning Mode | Execution Mode |
|---|---|---|
| Activity editing | Full drag-and-drop editor | Not available |
| Undo / redo | Available in session | Not available |
| Constraint warnings | Proactive on every edit | On-demand when delay is flagged |
| Recovery options | "What if" exploration available | Presented immediately on delay entry |
| Dependency chain view | Full visualization | Collapsed; immediate next only |
| Location configuration | Full edit | Read-only display |
| Group Photo Optimizer | Full editor | View only |
| Delay handling | Not applicable | Primary feature |
| Mark complete | Not applicable | Available but not relied upon |
| Emergency contacts | Accessible in questionnaire | One-tap access from main view |

---

## 6. Role-Filtered Views

### Owner (Photographer)

| Category | Access |
|---|---|
| Data visibility | Full — all activities, all notes, all people, all vendors |
| Editing permissions | Full — create, edit, delete, reorder, configure anchors and visibility |
| Change approval | Full — approves couple proposals; reviews collaborator changes under Review Required |
| Reporting / export | All PDF formats |
| Account / billing | Full |

---

### Planner — Collaborator

| Category | Access |
|---|---|
| Data visibility | Full timeline, all vendors, all people |
| Editing permissions | Full timeline editing; changes apply immediately under Review Required (owner is notified and can revert) |
| Change approval | Cannot approve couple proposals; own changes are logged for owner review |
| Reporting / export | All PDF formats |
| Account / billing | None |

### Planner — Co-owner

| Category | Access |
|---|---|
| Data visibility | Full timeline, all vendors, all people |
| Editing permissions | Full — same as owner for event content |
| Change approval | Can approve couple proposals; own changes apply directly |
| Reporting / export | All PDF formats |
| Account / billing | None (account management stays with owner) |

**Simple rule for MVP:** When inviting a planner, the owner chooses one: Collaborator or Co-owner. If unsure, default to Collaborator.

---

### Vendor (Team Member)

| Category | Access |
|---|---|
| Data visibility | Only activities where their role appears in the activity's visibility settings. No internal notes. No other vendor contacts. |
| Editing permissions | None — read-only |
| Reporting / export | Their filtered view as PDF |
| Account | None required — link-based |
| Status | Invited / Viewed / Confirmed |

Vendor sees: activity title, start time, duration, location, vendor-facing notes, their checklist items.

Vendor does not see: full timeline, other vendors' activities, questionnaire data, internal notes, family group detail.

---

### Client / Couple

| Category | Access |
|---|---|
| Data visibility | Full timeline in simplified display (time, activity, location — no constraint metadata, no internal notes). Their questionnaire sections. |
| Editing permissions | None direct — all changes are proposals requiring owner approval |
| Reporting / export | Couple's filtered PDF view |
| Account | Lightweight (magic link or Google sign-in) |

Couple sees: activity title, time, location; activities with couple-level visibility; their submitted suggestions and status; What's Changed Since Last Visit.

Couple does not see: internal photographer notes, vendor contact details, constraint metadata, Group Photo Optimizer editor.

---

## 7. Location Sharing — Planned Future Feature

Location sharing is a planned feature for a post-MVP release. It is documented here so that MVP design and data model decisions do not close the door on it.

### Purpose

Help vendors and team members on wedding day know where key people are. Detect when someone may be running late and prompt them privately before automatically alerting the team.

### Behavior

- Opt-in only. Each user individually controls whether their location is shared and can turn it off at any time.
- During Wedding Day Mode, participants who have opted in share their live location with the event team.
- The system estimates whether someone is on track to arrive at their next required location on time, based on travel distance and time.
- If someone appears to be running late, the system privately prompts only them first: "It looks like you may be running about 10 minutes behind. Do you want to update the team?"
- The user chooses:
  - Notify affected team members (sends delay alert only to people whose activities are impacted)
  - Update the timeline only (adjusts the internal timeline without notifying others)
  - Dismiss (no action taken)
- The event owner and co-owner can see delay-risk indicators for the event as a whole, but cannot see individual location data unless the person has shared it.
- The system does not automatically send notifications to anyone. Human approval is required before any message goes out.
- Location sharing automatically expires when the event date ends.

### Privacy Rules

- Never share location data with vendors unless the person has explicitly opted in.
- Never display raw location coordinates — only contextual delay risk ("appears to be running about 10 minutes behind").
- Location data is used only for delay detection during the event. It is not stored persistently after the event ends.

### MVP Decision

Treat as a post-MVP feature. Do not build location sharing infrastructure in V1 unless it can be implemented simply without delaying core MVP validation. Design the data model and event-participant architecture so that adding location sharing in V2 does not require restructuring.

---

## 8. MVP / V2 / Later

### MVP — Required for initial validation on real weddings

| Feature | Why it is MVP |
|---|---|
| Account creation and sign-in for professionals | Entry requirement |
| Lightweight couple sign-in (magic link + Google) | Couples need account access for questionnaire and proposals |
| Vendor link access (no account) | Required for every wedding — photographers share links with DJs and venues |
| Vendor link marketing prompt | Low-effort growth mechanism; builds vendor awareness |
| Vendor status tracking (Invited / Viewed / Confirmed) | Owner must know whether vendors have actually seen their timeline before the wedding day |
| Event creation with wedding template and smart defaults | Starting point for every event; smart defaults make first use immediate and low-friction |
| One shared questionnaire (owner fills, couple completes and updates) | Drives group photo optimizer and location intelligence |
| Emergency contact layer (questionnaire section 8 + one-tap access in Wedding Day Mode) | Safety requirement; required for Event Readiness Checklist |
| Expanded group photo participants (all relationships, not just immediate family) | Required for accurate optimizer output |
| Timeline editor: add, edit, reorder activities | Primary product surface |
| Dependency-aware activity movement | Proves Timeline Intelligence — the primary strategic moat |
| Anchor types: locked, preferred, flexible | Required for constraint engine to work |
| Location inheritance and auto travel blocks | Required for realistic wedding timelines |
| Activity fields: duration, minimum duration, priority, notes, visibility | Required for constraint evaluation |
| Constraint warnings (anchor, chain, duration, travel) | Without warnings, it is just a list editor |
| Group Photo Optimizer: auto-suggest, reorder, duration estimate, cross-group tracking | Secondary strategic moat; required for photographer validation |
| Review Required workflow: couple proposals require approval; collaborator edits apply immediately with owner notification and revert option | Fundamental to collaboration model; not a blocking approval queue |
| Wedding Day Mode with delay adjustment as primary feature | Core day-of experience; must be validated on real weddings |
| Recovery options presented after delay entry | Required for Timeline Intelligence to be meaningful on the day |
| Selective notifications (only affected parties, owner approves) | Delay handling is not useful if it spams everyone |
| Mark activity complete (secondary, not relied upon) | Available for photographers who want it; not a core behavior |
| Planner roles: Collaborator and Co-owner | Professional collaboration is required for planner market |
| PDF export: compact, full, vendor-filtered, group-photo-only, couple's view | PDF is the required emergency backup for the wedding day |
| Couple PDF download from their interface | Confirmed by founder |
| PDF download required before event date — Event Readiness Checklist item 3 | Safety requirement; system warns clearly if not downloaded |
| Event Readiness Checklist (7 items — not binary ready state) | Planning clarity requirement; guides owner through preparation step by step |
| What's Changed Since Last Visit (owner, planner, couple) | Required for collaboration — all parties need to know what changed since their last visit |
| Version history: undo/redo + automatic snapshots + full timeline restore + change log + version comparison summary | Required before photographers trust the system with live events |
| Free tier — 3 lifetime events | Required to control costs during validation |

---

### V2 — High Value, Post-Validation

| Feature | Notes |
|---|---|
| SMS / email notifications to vendors | Manually sharing links works for V1; notifications improve reliability in V2 |
| Venue profile database | Requires a separate venue-facing surface; useful for travel block pre-population |
| Offline PWA cache | Print backup covers offline safety for MVP; offline editing is V2 |
| Google Calendar one-way sync | Useful for couples and planners; not needed to prove Timeline Intelligence |
| Vendor location sharing (opt-in, delay detection, private prompts) | Planned feature per architect decision; add when core MVP is validated |
| QR codes for vendor links | Convenient; not blocking; add alongside location sharing or independently |
| Improved recovery option ranking (usage-informed heuristics) | V1 heuristics are sufficient; improves with real usage data |
| Custom branding add-on (paid) | Confirmed as post-MVP paid feature; requires billing infrastructure |
| Custom domain (paid add-on) | Same as above |

---

### Later (V3+)

| Feature | Deferred reason |
|---|---|
| Two-way Google Calendar sync | Requires careful conflict resolution; V3 |
| Outlook / Microsoft 365 sync | Corporate market; V3+ |
| Corporate event / conference templates | Phase 4 market |
| Production / call-sheet modules | Phase 5 |
| Advanced AI recovery engine (pattern-trained) | Requires real usage data across many events |
| AI-improved group photo sequencing | Heuristics are sufficient for validation; AI improves later |
| Questionnaire defaults / section-level guidance from past events | Deferred; names and contacts from past events will not be pre-filled |
| HoneyBook / Studio Ninja CRM import | Phase 3 |
| Zapier / Make connector | Phase 3+ |
| Enterprise permissions / team accounts / API | Phase 4 |
| Multi-photographer team accounts | Phase 2/3 when planner market is active |

---

## 9. Founder Decisions — All Confirmed

All items below are confirmed. No open questions remain before Lovable implementation.

| # | Decision | Status | Notes |
|---|---|---|---|
| 1 | Vendor access is link-based (no account required) | **Confirmed** | Marketing prompt included on vendor link landing. |
| 2 | Couple sign-in is magic link + Google (lightweight, not professional) | **Confirmed** | No plan selection, credit card, or settings on sign-in. |
| 3 | All couple changes are proposals requiring owner approval | **Confirmed** | Applies to questionnaire, timeline, family groups, vendors, key details. |
| 4 | Delay adjustment is the primary Wedding Day Mode feature; mark complete is secondary | **Confirmed** | System does not rely on mark complete. |
| 5 | Planner has two levels: Collaborator and Co-owner | **Confirmed** | Default to Collaborator when inviting. |
| 6 | Couple can download their own PDF | **Confirmed** | Available from the couple's interface. |
| 7 | QR codes are V2, not MVP | **Confirmed** | Unless trivially easy; share links are sufficient for MVP. |
| 8 | Questionnaire pre-fill from past events is deferred | **Confirmed** | No names or contacts from past events. Section-level guidance is a later feature. |
| 9 | Custom branding and custom domain are paid V2 features | **Confirmed** | Does not block MVP. |
| 10 | Location sharing is V2, not MVP | **Confirmed** | Data model must accommodate it. |
| 11 | Group Photo Optimizer covers both family and wedding party groupings | **Confirmed** | Questionnaire collects all participants, not just immediate family. |
| 12 | Group photo participants expanded to all relationships (extended family, chosen family, VIPs) | **Confirmed** | Not limited to parents and siblings. |
| A | **Collaborator approval rules:** Collaborator edits apply immediately under Review Required (not a formal approval queue). Owner is notified; can review in the change log and revert. No blocking gate for collaborators. Couple changes always require explicit approval. | **Confirmed** | Review Required is a notification model, not an approval gate. |
| B | **Event Readiness:** 7-item checklist — not a binary ready/not-ready state. Items: questionnaire complete, groups sequenced, PDF downloaded, no critical warnings, couple proposals resolved, at least one vendor link shared, emergency contacts entered. | **Confirmed** | Checklist drives pre-event preparation. Warning triggered if checklist incomplete within 7 days of event. |
| C | **Rollback scope:** MVP rollback = undo/redo (in-session) + automatic snapshots (at key milestones) + full timeline restore (with confirmation) + change log (every change, every user) + version comparison summary (before/after diff between any two snapshots). | **Confirmed** | All four components are MVP. Full-timeline restore, not activity-level rollback. |
| D | **Google Drive:** Architecture must be merged into Master Google Docs before Lovable implementation begins. Founder to copy confirmed content into `OnCue Master Document V2.gdoc` and `OnCue Founder Decisions Log.gdoc`. This document then serves as the implementation spec; Master Docs remain the strategic authority. | **Confirmed** | This is the required next step before Lovable begins. |
| E | **What's Changed Since Last Visit** is MVP. Shown to owner, planner, and couple when returning to an event after changes have been made. Plain-language summary. Dismissed by the user or auto-dismissed after 24 hours. | **Confirmed** | Required for collaboration awareness across all roles. |
| F | **Vendor status tracking (Invited / Viewed / Confirmed)** is MVP. Status visible on Vendor Role Management screen and Dashboard event card summary. Confirmed via one-tap on vendor link landing. | **Confirmed** | Owner needs this before the wedding day to know vendors are prepared. |
| G | **Emergency contact layer** is MVP. Questionnaire section 8. One-tap access in Wedding Day Mode. Data loaded offline when Wedding Day Mode is entered. Required for Event Readiness Checklist item 7. | **Confirmed** | Safety requirement. |
| H | **Mobile-first, one-handed operation** is a hard design requirement. Every day-of action completable with one thumb. Minimum 44×44pt touch targets. Critical actions in two taps maximum from main Wedding Day screen. | **Confirmed** | Governs all screen and interaction design decisions. |
| I | **PDF backup is a required emergency backup**, not optional. Persistent warning in Planning Mode if not downloaded before event date. Event Readiness Checklist item 3. Export screen shows last download date. | **Confirmed** | PDF is the safety net for the day. |
| J | **Smart defaults are required for every field.** A photographer who enters only event date and couple names must get a usable baseline timeline. All defaults are visible, labeled, and overridable. | **Confirmed** | Reduces first-event friction. Builds trust immediately. |

---

*This document is architecture and definition only. No application code, framework, database schema, or Lovable implementation has been started. All decisions are confirmed. The required next step before implementation is merging this architecture into the Master Google Docs (item D above).*
