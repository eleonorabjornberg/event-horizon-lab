# Event Horizon Lab

An interactive, physically grounded black hole in a single HTML file. A WebGL fragment shader traces light rays through the curved spacetime around a non-spinning (Schwarzschild) black hole, and a probe can be dropped in to show what a distant observer sees.

Built as the physics ground truth for a Reactor x Google World Models Hackathon project: the shader renders correct physics, and a real-time video-to-video world model can restyle it.

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
- **Readouts.** Horizon radius, light-crossing time, tidal pull, redshift, Hawking temperature and evaporation time, all as functions of mass.

## Known approximations

- Disk Doppler beaming uses a simplified special-relativistic factor times the static gravitational redshift.
- The probe's redshift is computed along a single radial line of sight.
- The amount of tidal stretch drawn is a log-scaled visual indicator; the tidal numbers are exact.
- Spinning (Kerr) black holes are not modelled.

## Using your own sky

"Use my own sky image" wraps any image around the sky as an equirectangular map and lenses it. This is the hook for live world-model frames: replace the uploaded image with a texture updated from a video stream every frame.
