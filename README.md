# Event Horizon Lab

An interactive, physically accurate black hole for teaching, in a single HTML file. A WebGL fragment shader traces light rays through the curved spacetime around a non-spinning (Schwarzschild) black hole, and a probe can be dropped in to show what a distant observer sees. Quantum effects are being added in stages on top of the general-relativity picture.

Live: https://eleonorabjornberg.github.io/event-horizon-lab/

## Run it

Open `index.html` in a browser, or serve it locally:

```
python3 -m http.server 8000
```

then go to http://localhost:8000.

## What it computes

- **Light bending.** Each pixel's ray is integrated backwards with x'' = −(3/2)·h²·x/r⁵ in units where the Schwarzschild radius r_s = 1 (the technique used by the Starless ray tracer). This produces the shadow (about 2.6 r_s), the disk image wrapped over and under the hole, and the thin photon ring.
- **Accretion disk.** From the innermost stable orbit (3 r_s) outwards, with temperature falling as r^(−3/4), Keplerian rotation and Doppler beaming.
- **The probe.** Radial free fall from rest at 10 r_s, integrated in the distant observer's time. It slows, reddens and fades at the horizon without crossing, while its own clock reaches the horizon in finite time.
- **Tides.** The probe stretches along its direction of fall according to the tidal pull across a 2 m body: spaghettified for a solar-mass black hole, intact for Sagittarius A*.
- **Readouts.** Horizon radius, light-crossing time, tidal pull and redshift, all as functions of mass.

## The quantum side

**Stage 1, Hawking radiation (built).**

- **Temperature and spectrum.** T = ħc³ / (8πGMk_B), about 6.17 × 10⁻⁸ K for one solar mass. The glow peaks (Wien's law) at a wavelength of about 16 horizon radii at every mass, and the panel names the band: radio for stellar holes, gamma rays for a mountain-mass one.
- **Power and lifetime.** P = ħc⁶ / (15360πG²M²) and t = 5120πG²M³ / (ħc⁴), both for photon emission.
- **Against the cosmic microwave background.** Holes colder than 2.725 K (heavier than about 4.5 × 10²² kg, roughly the Moon) absorb more than they emit today and are still growing.
- **The glow on screen.** Rays that end at the horizon return the Hawking colour, so the glow fills the shadow as a distant observer would see it. True colour between 1,000 and 40,000 K, false colour outside that range, brightness always exaggerated, and the panel says which.
- **Evaporation.** M(t) = M₀(1 − t/t_life)^(1/3), played over 24 seconds with a mass-time curve. Most of the life changes almost nothing; the end is sudden. The last second releases about 2 × 10²² J from about 230 tonnes of mass.
- **Mass range** now runs down to 10⁻²⁰ solar masses, with mountain-mass and Moon-mass presets, so hot, fast-evaporating holes can be explored.

**Stage 2, the Unruh effect (built).**

- **The effect.** A thermometer accelerating through empty space reads a temperature T = ħa / (2πck_B), about 4 × 10⁻²⁰ K for 1 g. One in free fall reads nothing.
- **Hovering above the hole.** Staying at a fixed radius r takes a proper acceleration a = GM / (r²√(1 − r_s/r)), which grows without limit at the horizon. A height slider (10⁻⁶ to 100 horizon radii above it) shows the thrust in g and the bath temperature, side by side with a falling probe at the same height.
- **Against the Hawking temperature.** The ratio is T_Unruh / T_Hawking = 1 / (ρ²√(1 − 1/ρ)) with ρ = r / r_s, the same at every mass. Close to the horizon the bath matches the Hawking glow as measured at that height, T_H / √(1 − r_s/r); far out it fades and the Hawking glow itself is what remains.
- **Hover, then let go.** "Hover a probe here" holds the probe on rockets, with a halo in the colour of its bath and its clock running slow by 1/√(1 − r_s/r). "Let it fall" releases it from rest at that height: the bath readout drops to none at once, and the probe falls in on its own clock while its image freezes at the edge.

**Stage 3, the information paradox (planned).** A Page-curve panel tied to the evaporation run: the entanglement entropy of the radiation rising, then, if information is preserved, turning over at the halfway point.

## Known approximations

- Disk Doppler beaming uses a simplified special-relativistic factor times the static gravitational redshift.
- The probe's redshift is computed along a single radial line of sight.
- The amount of tidal stretch drawn is a log-scaled visual indicator; the tidal numbers are exact.
- Spinning (Kerr) black holes are not modelled.
- Hawking emission counts photons only and ignores greybody factors, so the power is too low and the lifetime too long for small holes, which also emit neutrinos, gravitons and heavier particles once hot enough.
- Evaporation ignores the cosmic microwave background, so it runs even for holes that are growing today; the panel says so.
- The on-screen Hawking glow is uniform in colour and scaled to be visible; the real glow is far too faint to see.
- The Unruh bath uses the hovering probe's local proper acceleration only. The falling probe is shown with no bath, leaving out the faint Hawking glow passing it. The halo around a hovering probe is false colour outside 1,000 to 40,000 K and always exaggerated.
- Height above the horizon is the Schwarzschild coordinate r − r_s, not the distance a ruler would measure.

## Using your own sky

"Use my own sky image" wraps any image around the sky as an equirectangular map and lenses it. A photo of a familiar place shows how strongly the black hole bends everything behind it.
