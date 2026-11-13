# Japanese Dream House — design and verification ledger

**Project:** Yama no Ie · Japanese Dream House  
**Type:** One-storey Wa-modern house for two, with engawa and Japanese garden  
**Canonical source:** [`src/apartments/japanese-dream-house.js`](../src/apartments/japanese-dream-house.js)  
**Model:** 12.3 MB self-contained three.js walkthrough at `dist/japanese-dream-house.html`  
**Plan sheet:** JDH-A101 — [`japanese-dream-house-plan.svg`](../shots/jdh/japanese-dream-house-plan.svg) / PNG  
**Required views:** [`shots/jdh/`](../shots/jdh/) and contact sheet

---

## 1. What was built

A single data-driven house description produces the architecture, gable roof,
cedar cladding, engawa, interiors, furniture, garden and lighting. The same
coordinate system is used for the plan, the section, all elevations, the
first-person walkthrough and every camera preset.

The visual language follows the approved reference:

- A compact rectangular house, one room deep in the living and bedroom wings.
- A low charcoal gable roof with the ridge east–west and deep eaves over a south
  engawa.
- Warm cedar board-and-batten cladding, dark bronze window frames, a stone
  plinth and a recessed dark entrance.
- Warm-white plaster, pale oak floors and exposed timber rafters inside.
- A hinoki soaking tub, a separate WC, a compact kitchen with an oak dining
  table, a low bed and a utility core.
- A private garden with lawn, stepping stones, a stone lantern, mossy boulders,
  a cherry, maples, clipped hedges and low warm path lights.
- No neighbouring houses are modelled.

---

## 2. Dimensions and the reading of the reference

The plan dimensions in the reference conflict slightly with the area labels.
The following reading was adopted and is documented here rather than silently
resolved:

- **Internal envelope: 8.00 m (east–west) × 8.50 m (north–south) = 68.0 m²**
- **External footprint: 8.36 m × 8.86 m** after the 180 mm cedar walls.
- **Net room area: 65.12 m²**; the remaining 2.88 m² is internal wall/partition
  footprint inside the 68.0 m² envelope.
- **External roofed footprint:** 9.52 m × 11.28 m including the 1.20 m eave and
  0.58 m gable overhangs.

Why this reading: the approved image labels 8.0 × 8.5 m and “68 m² (≈ 8 × 8.5)”.
Treating 8.0 × 8.5 as the internal envelope is the only way both statements can
be true at once. The drawing is therefore dimensioned 8.36 × 8.86 externally
and 8.00 × 8.50 internally.

### Room schedule (derived geometry)

| Room | Internal size | Net area | Reference label | Note |
| --- | ---: | ---: | ---: | --- |
| Bedroom | 4.40 × 3.60 m | 15.84 m² | 15 m² | master bedroom for two |
| Living Room | 4.40 × 4.78 m | 21.03 m² | 20 m² | open to kitchen; south glazing and west window |
| Kitchen + Dining | 3.60 × 2.83 m | 10.19 m² | 12 m² | open-plan social space; the dining table extends the living-side room visually |
| Entrance | 0.98 × 1.83 m | 1.79 m² | — | genkan with stone floor; no cabinet in the clear path |
| Laundry / Storage | 2.50 × 1.83 m | 4.58 m² | 6 m² | washer and tall storage; east service door |
| Bathroom | 2.23 × 2.15 m | 4.79 m² | 5 m² | ofuro, vanity, north garden window |
| Linen Store | 1.13 × 2.15 m | 2.43 m² | — | accessed from the bathroom; extra storage |
| Hall | 1.26 × 1.33 m | 1.68 m² | circulation | links kitchen, bathroom and WC |
| Toilet | 2.10 × 1.33 m | 2.79 m² | 2 m² | separate WC, hand basin and east window |
| **Total room area** | | **65.12 m²** | | partitions make up the rest of the 68.0 m² |

The reference’s laundry / storage (6 m²) and the added linen store together give
7.0 m² of utility storage. The kitchen is 10.2 m² inside the fixed envelope; the
reference’s 12 m² label is treated as indicative because the open table zone
reads together with the living room. These are recorded as approximations, not
silent design changes.

---

## 3. Planning and circulation

North is −Z. The long glazed facade and engawa face south (+Z). The roof ridge
runs east–west so the long drainage eave faces the garden and the cedar-clad
gables close the east and west ends.

```
                 NORTH / rear
   bedroom   | bath | linen store
   ----------+------+-------------
             | hall | toilet
   living    |      | kitchen + dining
   (west)    | entry| (east)
             |      | laundry / storage
                 SOUTH / garden
```

- **Public route:** front door → entrance → living room → open kitchen/dining.
- **Private route:** living room → bedroom door.
- **Service route:** kitchen → hall → bathroom / WC. The linen store opens off
  the bathroom.
- **Second exit:** the laundry has an east service door to the garden.
- **Garden exit:** a full-height five-panel sliding glazing opens on its centre
  bay to the engawa; the entrance door opens onto the same deck.
- Doors in the visualisation are interactive. The walk test checks every room is
  reachable through the collider space with the doors open.

---

## 4. Openings schedule

All positions are in the derived model; the plan drawing uses the same values.
Widths are clear structural openings.

### Exterior

| Opening | Wall | Width | Sill / head | Notes |
| --- | --- | ---: | --- | --- |
| `livingGlazing` | south | 3.70 m | 0.00 / 2.40 m | 5 panels, centre bay open |
| `frontDoor` | south | 0.90 m | 0.00 / 2.20 m | hinged cedar door to engawa |
| `laundryWindow` | south | 0.90 m | 1.18 / 1.98 m | high utility window |
| `bedWindowN1` | north | 1.70 m | 0.78 / 2.23 m | bedroom garden window |
| `bedWindowN2` | north | 1.10 m | 0.78 / 2.23 m | second bedroom window |
| `bathWindow` | north | 1.70 m | 1.02 / 1.97 m | over the ofuro |
| `bedWindowW` | west | 2.00 m | 0.78 / 2.33 m | bedroom west window |
| `livingWindowW` | west | 2.30 m | 0.50 / 2.55 m | low lounge window |
| `linenWindow` | east | 0.65 m | 1.35 / 1.90 m | slot window |
| `toiletWindow` | east | 0.70 m | 1.32 / 1.94 m | privacy height |
| `kitchenWindow` | east | 1.35 m | 1.02 / 2.10 m | over the sink run |
| `laundrySideDoor` | east | 0.85 m | 0.00 / 2.05 m | service door to garden |

### Interior

| Opening | Between | Width | Height | Type |
| --- | --- | ---: | ---: | --- |
| `bedroomDoor` | bedroom / living | 0.90 m | 2.08 m | hinged |
| `bathDoor` | bath / hall | 0.72 m | 2.02 m | hinged |
| `hallDoor` | kitchen / hall | 0.80 m | 2.02 m | hinged |
| `toiletDoor` | hall / toilet | 0.70 m | 2.00 m | hinged |
| `linenDoor` | bath / linen | 0.65 m | 1.98 m | hinged |
| `laundryDoor` | entrance / laundry | 0.75 m | 2.02 m | hinged |
| `entryArch` | entrance / kitchen | 0.82 m | 2.25 m | cased opening |

The reference does not dimension every internal leaf. These widths follow the
ergonomic minimums in the foundation standards while keeping the clear
circulation path used by the player collision test.

---

## 5. Roof, section and envelope

- Gable roof; ridge east–west at z = 0.
- Pitch **18°**; wall lift 0.16 m; eave overhang 1.20 m; gable overhang 0.58 m.
- Wall plate 2.70 m; ridge approximately **4.30 m** above finished floor.
- Roof planes have a **charcoal matte finish**, standing seams, deep fascia and
  a dark gutter line.
- Exposed cedar rafters at 0.88 m centres and a ridge beam remain visible under
  the timber ceiling.
- The ceiling follows the roof as a warm oak plane at −0.15 m from the roof
  underside; upper wall infill closes each room to the sloping ceiling so the
  plan remains nine rooms and not one open attic.
- Windows and doors are cut from the derived walls by the same opening engine
  used by the rest of the project, so the 3D openings and the plan symbols are
  driven by one set of dimensions.
- A cedar board-and-batten skin, corner boards, stone plinth, privacy screen,
  eave fascia, rafters and engawa are built by `src/arch/shell.js`.

---

## 6. Materials

| Element | Finish | Notes |
| --- | --- | --- |
| Exterior walls | `cedarExterior` | warm natural cedar over vertical board battens |
| Accent battens / screens | `cedarBatten`, `cedarDark` | same cedar family, darker tone |
| Interior walls | `warmPlaster` | warm white, fine trowel character |
| Floors | `oakFloor`, `oakFloorWarm` | natural pale oak |
| Ceiling and rafters | `ceilingOak`, `cedarBeam` | timber vault |
| Roof | `roofCharcoal` | charcoal matte metal |
| Window frames | `bronze` | dark bronze / charcoal |
| Kitchen and joinery | `lightOak`, `kitchenOak` | pale oak |
| Worktops | `counterStone`, `stoneTop` | honed warm stone |
| Bath | `bathStone`, `hinoki`, `hinokiDark` | stone tile and hinoki tub |
| Deck | `deckTeak` | warm timber |
| Garden | `gardenStone`, `gardenStoneDark`, `moss` | stone, moss, grass |
| Landscape light | `deckLight`, `lanternGlow` | warm low-level light |

No new dominant colour family is introduced outside the approved cedar / oak /
warm-white / charcoal / bronze / garden palette.

---

## 7. Garden and environment

- Managed lawn around the house; no neighbouring buildings.
- Meandering stepping-stone path from the engawa to a timber garden gate.
- Stone lantern with a warm integral light.
- Cherry, maples, broadleaf trees and a pine, plus a clipped hedge boundary at
  24 m and a distant mature tree line for privacy.
- Mossy boulders, low clipped shrubs, ornamental grass tufts and groundcover.
- Warm path bollards, deck step lights, string lights under the eave and a
  lantern light.
- Player can leave the house through the front door or the centred glazing bay
  and walk on the lawn and deck. The property boundary is a collider; no edge
  of the world can be walked off.

The garden layout is an architectural interpretation of the reference; exact
plant positions are not recoverable from the poster.

---

## 8. Camera views and in-app gallery

`window.__G.apartment.shots` defines twelve cameras. They are also exposed in
the HUD views menu (key **V**), so the required views are not only files but
live camera positions in the interactive model.

| View | File | What it verifies |
| --- | --- | --- |
| Hero | `japanese-dream-house-hero.png` | south-east approach, roof, screen, deck |
| Front | `japanese-dream-house-front.png` | garden facade, glazing, entrance |
| Rear | `japanese-dream-house-rear.png` | bedroom and bath windows |
| Left | `japanese-dream-house-left.png` | west gable, living window |
| Right | `japanese-dream-house-right.png` | east windows and service door |
| Bird’s-eye | `japanese-dream-house-aerial.png` | roof geometry, garden context |
| Living | `japanese-dream-house-living.png` | timber vault, glazing, furniture |
| Kitchen + Dining | `japanese-dream-house-kitchen.png` | oak kitchen, table, hood |
| Bedroom | `japanese-dream-house-bedroom.png` | bed, joinery, north/west windows |
| Bathroom | `japanese-dream-house-bathroom.png` | ofuro, window, stone, vanity |
| Garden + veranda | `japanese-dream-house-veranda.png` | engawa, deck furniture, garden |
| Garden | `japanese-dream-house-garden.png` | path, lantern, house from the lawn |

Plan sheet JDH-A101 is the architectural floor plan at 1:50. It is generated by
`tools/jdh-plan.mjs` from the same apartment file (walls, openings and scheduled
fixtures).

---

## 9. Verification — final run

### Unit tests

```bash
npm test
# 134 pass, 0 fail
```

The house contributes eight tests in
[`test/japanese-dream-house.test.js`](../test/japanese-dream-house.test.js):
description validation, internal/external dimensions, room programme, opening
set, roof geometry, palette, placement bounds and exterior-opening check.

### Browser quality gate

```bash
node tools/check-jdh.mjs
```

Latest run **ALL CHECKS PASS**:

- page / shader errors: none
- WebGL2 context: yes
- GI: available, bake **3.2 s**
- gable roof, timber ceiling and cedar shell present
- internal envelope **8.00 × 8.50 m**; external footprint **8.36 × 8.86 m**
- all nine rooms present; bedroom 15.8 m², living 21.0 m², bath 4.8 m²
- all nominated external and internal openings present
- interactive doors: **8/8** open, close and update their colliders
- flood-fill with the player’s 0.26 m radius reaches every room
- front door and central glazing bay both connect house and garden
- boot to ready **≈7 s**; interactive frame rate **56–58 fps** in headless Chrome
  (1440 × 900, Metal-backed ANGLE)

### Plan consistency

- Wall, opening and room counts come from `derivePlan()`.
- The floor plan, 3D walls and first-person colliders are all built from the
  same room rectangles and opening definitions.
- Cedar battens are cut around the 19 openings rather than painted over; all
  external openings survive the cladding pass.
- Every required camera is a fixed point in the same building model.

### Render set

```bash
node tools/shots.mjs japanese-dream-house shots/jdh
```

12 × 1600 × 1000 PNGs, plus the floor plan and the contact sheet.

---

## 10. Assumptions and unresolved decisions

These are explicitly documented rather than hidden:

1. **Dimension interpretation.** 8.0 × 8.5 m is taken as internal because it
   reconciles the 68 m² area note. The external footprint therefore measures
   8.36 × 8.86 m.
2. **Room-label differences.** Kitchen + Dining is 10.2 m² rather than 12 m²,
   and Laundry / Storage is 4.6 m² rather than 6 m². The fixed envelope and
   circulation are prioritised; the separate Linen Store brings total utility
   storage to 7.0 m². The WC is 2.8 m² rather than 2 m² to keep a usable
   hand-basin and a legal-feeling door swing.
3. **Internal partition layout.** The reference plan is low-resolution at the
   partition level. The exact service-core arrangement (bath / hall / WC /
   linen) is an architectural inference made to fit a coherent 8 × 8.5 m plan.
4. **Bathroom access.** The ofuro was sized to 1.32 m wide and the vanity moved
   to the south wall so that the room and the linen cupboard remain walkable.
5. **Roof details.** Pitch, louvred gable vent and standing-seam appearance are
   inferred from the reference photograph. No structural design is claimed.
6. **Garden.** Plant species, tree positions, lantern placement, path shape and
   the exact lawn/hedge dimensions are interpretations. Foliage is stylised,
   not a photogrammetric asset.
7. **Furniture and styling.** The kit furniture is representative of the
   reference, not measured from it. No appliance or plumbing schedules are
   supplied beyond the visible fixtures.
8. **Construction documentation.** This is a visualisation model, not a
   permit/construction set. Structure, drainage, electrical, mechanical,
   waterproofing and joinery details are illustrative.
9. **Screens and privacy panel.** The tall cedar privacy screen beside the
   entrance is an inferred feature consistent with the reference’s timber
   screens.
10. **No human sign-off yet.** The render set and plan are ready for review;
    the final material and planting selections are subject to the client’s
    approval.

---

## 11. File map

```
src/apartments/japanese-dream-house.js   canonical house description
src/arch/shell.js                        gable roof, cedar skin, ceiling, engawa, screens
src/kit/japanese-garden.js               garden, trees, stones, lantern, path, lights
src/kit/bathroom.js                      ofuro + wc basin additions
src/kit/laundry.js                       washer + drying rail
src/kit/decor.js                         slat feature panel
src/kit/lighting.js                      wall lantern
src/engine/gi.js                         configurable lightweight GI bake
tools/jdh-plan.mjs                       plan sheet JDH-A101
tools/check-jdh.mjs                      house quality gate
test/japanese-dream-house.test.js        pure unit checks
dist/japanese-dream-house.html           self-contained walkthrough
shots/jdh/                               required views, plan, contact sheet
```

Commands added to `package.json`:

```bash
npm run build:jdh
npm run plan:jdh
npm run shots:jdh
npm run check:jdh
```

---

*Revision 2026-11-13. Model, plan, verification and screenshots are generated
from the same source file; the views are not independent designs.*
