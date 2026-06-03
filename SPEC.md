# TRIPLE MATCH 3D — Build Spec (source of truth)

Mobile-first H5 casual game, deployed on GitHub Pages. Vanilla ES modules, no build step, WebGL2.

## 1. Stack
- Three.js (3D), postprocessing via `EffectComposer`.
- (Planned) Rapier3D for physics where it adds juice.
- GSAP for tween/timeline animation.

## 2. Art direction
- **Claymorphism** — soft, rounded, glossy "jelly" tiles. Crisp & readable, **NOT** glary/bloom-washed, **NOT** blurry.
- Core palette: `#FF6B9D` (pink) · `#FFC75F` (gold) · `#4ECDC4` (teal), extended with vivid clay variants.
- Background: dark gradient `#1a1a2e → #16213e`.
- HDRI/`RoomEnvironment` env map + AO; bloom only on bright highlights (subtle), not whole tiles.
- Materials: `MeshPhysicalMaterial` clearcoat (+ transmission where it reads as jelly).
- Layout feel: **roomy, comfortable spacing** — never cramped, tiles not stuck together.

## 3. Juice ("Juice it or lose it") — every action = visual + audio + haptic < 1 frame
- merge/match: ~24 sparks + shockwave ring + bloom flash + trauma shake (scaled by tier).
- post FX: bloom, light chromatic aberration, vignette, DoF.
- squash & stretch; `easeOutBack` on spawn.

## 4. Animation (GSAP)
- UI 150–300ms; hero/board 400–600ms; spring easings.

## 5. Audio (Web Audio)
- Separate music / SFX buses.
- Pitch ladder per merge/match step; random pitch ±5%.
- Layered BGM; handle autoplay policy (unlock on first gesture).

## 6. UX
- Load < 2s with a loading screen + progress.
- Haptics (`navigator.vibrate`).
- Portrait orientation, safe-area insets.

## 7. Performance
- 60fps on mid-range Android with ~50 on-screen objects.
- Object pooling.
- Quality tiers (auto-downgrade when fps drops).
- Assets webp/KTX2; bundle < 2MB.

## Definition of Done
- [ ] Holds 60fps with 50 objects on screen.
- [ ] Every merge/drop/combo has visual + audio + haptic feedback.
- [ ] Plays smoothly under 4× CPU throttle.

## Layout research (pending)
Deep-dive on layout trends for this genre: best themes, top/bottom composition,
item size & spacing that players prefer → drives the layout redesign.
