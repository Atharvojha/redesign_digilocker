# Polish plan — merged from audit-emil.md (E#) and audit-apple.md (A#)

Backup of the pre-polish build: `archive/v1.html`. Only one agent edits `index.html` at a time.
Hard constraints: single file, vanilla HTML/CSS/JS, fictional data only, "Concept" label visible on every screen at every width, no official emblem.

## Batch 1 — Foundations (fix what's wrong)
1. **Fonts**: load Plus Jakarta Sans variable axis `wght@400..800` so 550/650/750 render. (E3, A4)
2. **Type scale in rem** (respects user font size), 9 tokens, tracking tied to size; kill half-pixel sizes. (E2, A30)
3. **Radius tokens** + concentric radii (inner = outer − padding); focus ring drawn on `.wc`, global focus rule without forced radius. (A31, E30)
4. **Contrast**: darken `--c2` for vehicle/education/certificates + bottom scrim on `.wc`; move sheen off the badge; `--text-3` light `#686a80`, dark `#8b8da4`. (E1, E17, A13)
5. **Card craft**: edge highlight + thickness inset shadows, subtle SVG grain, per-document colour within category family, short issuer names on the card face (full in sheet / `title`). (E10, E11, A12)
6. **Stacks read as stacks at rest**: l1 `translateY(9px) scale(.95) opacity .6`, l2 `translateY(17px) scale(.9) opacity .35`, brightness .92; fan slightly on hover. (E12, A3)
7. **Concept label on mobile app screens** (do not hide `.logo-tag`; compact it) + short concept banner on landing ≤520px. (A1, E25)
8. **iOS press states**: passive `touchstart` listener. (A2)
9. **Safe areas + dvh**: toaster above tabbar with inset, sheet last-child padding, topbar top inset, `dvh` everywhere. (A10, A11)
10. **Dark elevation**: `--surface-elev`, 1px hairline + inset top highlight on panels/popovers/palette, darker dark scrim. (E9, A23)
11. **Materials**: translucent topbar/tabbar (blur 20–24, saturate 1.8), scroll-edge border only when scrolled (also `.lp-head` inside sheets); tabbar active indicator. (A21, A22)
12. `html{scrollbar-gutter:stable}`. (E18)
13. **Loading ≠ disabled**: `aria-busy` style keeps full opacity; animate button width on label change. (A18)
14. **Hit targets**: invisible hit-slop (`::after inset:-6px`) on small controls; coarse-pointer sizes. (A32, E23)
15. **Reduced motion**: spinners keep spinning; popover no scale; `prefers-reduced-transparency`, `prefers-contrast`. (A33)
16. **Microcopy/data bugs**: revoke text for QR shares ("Anyone holding this QR…"), non-person recipient glyph instead of initials, "Change" → "Not your state?" focusing the select, stack lists newest-first, mask `INC•••••345`, grouped phone number, Drive meter 0 at 0 B. (A34)
17. **Theme toggle icon** sun/moon + view-transition theme crossfade. (E21, E32)
18. **Wallet hierarchy**: "Ready to add" becomes a slim expandable strip (mobile: horizontal suggestion chips) so cards are above the fold. (E4)
19. **Sheet redundancy**: one-line verified row under the card, Share as primary full-width button + 3 secondary tiles. (E13, E14)
20. **Stagger** capped per section (max 6 × 35ms), starts after sign-in modal exit. (E31, A17)
21. **Toasts**: Sonner-style stacked deck, expands on hover, evict with exit transition, dark-mode surface styling, swipe to dismiss. (E19, A10)
22. **Palette**: Suggested + Actions first when empty, stacks collapsed under parent, hover selects, footer key hints. (E20, A35)
23. Landing lower half less template-y: steps as a strip with mini UI illustrations, stat count-up on first view, varied icons for "New", drop the meaningless "New" tag; mobile hero shows 2 cards + 1 chip. (E24, E26, E27, A14)

## Batch 2 — Motion system (feel physical)
1. **Spring helper** (`response`/`damping`, velocity-seeded, retargetable) + rubber-band + momentum projection. (A9)
2. **Bottom-sheet gestures**: drag from grabber + header + body-at-scrollTop-0, release velocity from last 80ms, rubber-band upward (fill gap with `::after`), backdrop opacity tracks drag, spring hand-off. (A5)
3. **Content swaps**: FLIP panel height (380ms drawer curve); modal anchored to top so it only grows down; **directional push/pop** for drill-in vs Back (restore list scroll on Back). (E7, E8, A6, A7)
4. **Exit asymmetry**: drawer exit 280ms on `--ease-drawer` (no 168px first-frame jump); `closeAll()` animates. (E6, A8)
5. **Layout FLIP on render(false)** for filter/add/remove/revoke; focus restored sensibly. (A15)
6. **Route transitions** via View Transitions (fade + 6px rise), with fallback. (A16)
7. **Micro-interactions**: hold-to-remove with solid fill + label inverts + tension scale + "Keep holding…"; reveal unblur + draining 30s auto-hide underline; iOS-sized switch with stretching knob; seg press state; OTP focus follows autofill + digit pop + success green; fetch error placed under input + shake; "Show me where" grid-rows reveal. (A19, A20, A26, A27, A28, E35)

## Batch 3 — Breakthrough moments (pick these four; both agents converged on them)
1. **Living card**: the tapped card *is* the sheet hero — FLIP clone flies from grid slot into the sheet and back on close; on mobile the app behind scales to .94 with rounded corners and dims, bound to drag progress; a second sheet pushes the first back. (E-idea1, A-idea1, A-idea5, A24)
2. **Holographic verified seal + light-reactive tilt**: foil conic-gradient seal replaces the "Verified" pill; pointer-driven spring tilt ±6° with specular highlight on fine pointers; one shimmer on touch; static under reduced motion. (E-idea2, A-idea2)
3. **Recipient lens + Present mode**: Share modal shows a mini document where switched-off fields get redaction bars (clip-path sweep), "18+ ✓" stamp for Aadhaar, rolling count; Create flips the lens to the QR; QR gets a draining expiry ring; full-screen Present mode with wake lock and a simulated "Scanned by …" confirmation after ~4s. (E-idea3, A-idea3, A-idea4)
4. **Arrival moment**: successful fetch → card travels from the success hero into its wallet slot as the sheet closes, seal stamps on (scale 1.3→1, rotate −12°→0), suggestion strip shrinks. (E-idea5)

Stretch (only if everything above is solid): **Wallet deck mode on phones** (Apple-Wallet overlapping pile, tap to lift). (E-idea4, A-idea1)

## Verification for each batch
No console errors; 375 / 768 / 1440 widths, light + dark, reduced motion emulated via CSS check; no horizontal scroll; every flow from the previous test pass still works (search → sign-in → fetch error/success, stack drill-in/back, share QR/link/user, revoke, hold-to-remove + undo, palette, drive).
