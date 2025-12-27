# Ripple Shader Specification

## Goal
Create a liquid-like surface that communicates movement, collision, and depth through distortion and ripple propagation.

---

## Technical Approach (Unity URP)
Screen-space refraction driven by a dynamic ripple heightfield.

---

## Buffers
- Ripple Height RenderTexture (ping-pong A/B)
- Optional normal map derived from heightfield

---

## Inputs to Heightfield
### Player Movement
- Soft Gaussian impulses stamped along movement path
- Strength scales with velocity

### Wall Collision
- Sharper impulse at collision point
- Higher amplitude than movement ripples
- Brief edge glow on contact

---

## Ripple Simulation Step
Each frame:
- Sample neighbouring pixels
- Apply wave propagation
- Apply damping
- Write to alternate buffer

Key parameters:
- propagationSpeed
- damping
- impulseStrength
- collisionBoost
- noiseFloor
- maxAmplitudeClamp

---

## Rendering
- Use ripple normals to distort screen UVs
- Subtle specular highlight on steep slopes
- Collision proximity increases local contrast

---

## Failure Effect
- Invert ripple field briefly
- Collapse distortion inward
- Audio low-pass sweep
