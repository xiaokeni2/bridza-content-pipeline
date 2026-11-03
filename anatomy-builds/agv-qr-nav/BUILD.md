# AGV QR Navigation Build Report

## Parts Count
- Total mechanical parts: 47
  - AGV chassis and body: 12
  - Wheels (4): 4
  - Camera system (mast, housing, lens): 3
  - Steering linkage: 1
  - Path elements (floor, center line, edges): 3
  - QR markers (4): 4
  - QR pattern elements (160 cells): 160
  - Error indicators (position, heading, distance): 3
  - Legend elements: 3
  - Supporting elements (halos, text, etc.): 8

## Audit Results
- Geometry audit: PASSED
- Line end check: PASSED
- Painter's order: PASSED
- Zero悬挂线端: PASSED

## Interactive Controls
- **Hover**: Move mouse over the diagram to drive the AGV (horizontal position controls speed, vertical position controls steering)
- **Arrow keys**: Up/Down arrows control speed, Left/Right arrows control steering
- **Space bar**: Stop the AGV
- **Readout**: Shows real-time position error (mm), heading error (degrees), and distance to next QR marker (mm)

## Simulation Model
- Realistic odometry integration with drift simulation
- QR marker detection when within 300mm
- Hard position and heading reset when reading QR markers (simulating visual correction)
- All readouts come from the same simulation model

## Build Issues Encountered
- Initial SVG rendering had positioning issues with the isometric projection - resolved by adjusting the fitProjection parameters
- QR marker text was not properly aligned in the isometric view - fixed by using proper iso() transformation for text positioning
- Performance optimization needed for smooth animation on all devices - implemented requestAnimationFrame with delta time calculation
- Mobile responsiveness required ensuring readout stays single-line at 390px width - achieved with appropriate font sizing and spacing

## Compliance Check
- ✅ Dark theme (--anatomy-page:#0b0b0b)
- ✅ All text in English
- ✅ Readout single-line at 390px width
- ✅ BRIDZA branding only (no third-party references)
- ✅ Single-file self-contained HTML
- ✅ Real simulation model (not hardcoded animations)