# RescueFlow

Interactive emergency-response training prototype for Almaty. All incidents, teams, restrictions and shelter data are fictional. No connection to emergency services or government systems.

## Run

Node.js 22+ and pnpm:

```sh
pnpm install
pnpm dev
```

Open the local URL printed by Vite. `pnpm build` checks TypeScript and creates `dist/`.

## Demo walkthrough

1. Launch Emergency Simulation. Five reports arrive at 4.5-second intervals. Pause/resume or reset as needed. Reset before choosing another scenario.
2. Open an incident on the map or feed. Review the transparent rules and missing information.
3. Choose and confirm the priority. Approve a compatible available unit. Restricted connections require route verification and cannot be approved in this MVP.
4. Change processing status to In Progress, then Resolved. The unit becomes available again.
5. Inspect Analytics and transfer supplies in Resource Management.

State persists in browser localStorage. Settings offers a demo reset. RU/EN switches main navigation and workflow labels; some operational details remain English in this prototype.

## Architecture

- `src/model.ts`: types, fixtures, priority rules, Haversine distances and eligible-unit ranking.
- `src/Map.tsx`: Leaflet map, markers, popups and approximate connection lines.
- `src/main.tsx`: state, incident editor, dispatcher workflow, inventories, simulation and Recharts analytics.
- `src/style.css`: responsive dark command-center interface with Tailwind and Radix dialog primitives (shadcn-compatible styling).

Rule priority: immediate danger +4; 10+ affected people +3, 1–9 people +1; earthquake hazards +1. Critical >=6, High >=3, otherwise Medium. Verification gaps are shown without fabricating confidence scores. Resource availability is a separate recommendation constraint, never a reason to deny assistance or lower urgency.

Tiles require internet (OpenStreetMap); no API keys are needed. Markers and all local workflows remain available if tiles fail. Distance is straight-line, not road distance or ETA. Analytics uses actual report timestamps and current statuses, not historical resolution telemetry. Shelter occupancy is a fixed demo fixture; inventories are editable through transfers. Backend and authentication are not part of this local MVP.

