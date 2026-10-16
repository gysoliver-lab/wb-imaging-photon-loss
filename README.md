[github_README_wb_imaging_photon_loss.md](https://github.com/user-attachments/files/33522092/github_README_wb_imaging_photon_loss.md)
# From Membrane to Chip: Where Did the 100 Photons Go — Sources of Signal Loss in Chemiluminescence Imaging

**TL;DR** — Chemiluminescence radiates in all directions; a lens-based imager only captures the cone of solid angle directly in front of the lens (set by numerical aperture and focal length), so even a wide-angle lens collects **less than 1%** of emitted photons — over 99% are lost before reaching the sensor. Contact imagers remove the lens and the gap (optical path 0 mm), raising collection efficiency by roughly **two orders of magnitude**; reported comparisons show a 0.1 s contact exposure detecting a 1/500 antibody-dilution band that a 60 s lens-based exposure on the same membrane still missed. This is a property of the acquisition geometry, not a fault of any single instrument.

## Contents
1. The path a photon takes in one chemiluminescence image
2. Why long exposure is the only option (and what it costs)
3. A different structure: let photons skip the lens
4. Mapping the principle to what you see at the bench
5. What this principle does NOT explain
- FAQ
- References

## 1. The path a photon takes in one chemiluminescence image

Break the acquisition path into five steps and watch where loss occurs:

1. **Substrate reaction emits light.** HRP on the secondary antibody catalyzes the substrate and emits visible light. The issue: light does not travel in one direction.
2. **Photons radiate omnidirectionally.** This is the defining feature of chemiluminescence — light above, below, and to the sides of the band forms a full spherical radiation field.
3. **A small fraction heads toward the lens.** How much depends on the solid angle the lens can "see."
4. **The lens focuses photons onto the chip.** Each air–glass interface reflects away part of the light; multiple lens elements add transmission loss.
5. **The chip converts light to signal, software renders the image.**

Loss concentrates in steps 3 and 4. Steps 1–2 are reaction physics, independent of the instrument; step 5 is signal processing, unrelated to photon count. The only parts an instrument can change are steps 3 and 4. And how much step 3 captures is fixed by geometry: because chemiluminescence is omnidirectional, any lens "looking at the membrane from a distance" is bound by the same ceiling — regardless of brand or model.

## 2. Why long exposure is the only option (and what it costs)

With few photons arriving per second, the instrument can only accumulate over time to reach an acceptable signal-to-noise ratio. That is why lens-based imaging often needs tens of seconds to ten-plus minutes — not because it is "waiting" for a signal, but because so little arrives each second.

But lengthening exposure simultaneously amplifies another problem: strong bands hit the saturation ceiling first and blow out to white, while weak bands are still buried in noise. Capturing both ends of a single membrane commonly means taking several exposures at different times and stitching them into a high-dynamic-range (HDR) image.

One easily overlooked detail: a sensor's response is **not strictly linear** across exposure times, especially near saturation. A stitched HDR image is a composite, and for quantitative work it is not equivalent to a single true acquisition. This is a limit of the stitching method itself, not of any particular instrument.

## 3. A different structure: let photons skip the lens

If loss comes from the "lens" and the "distance," what if we remove both?

In contact chemiluminescence imaging, the sensor chip sits directly over the membrane — photons pass through no lens and cross no gap before reaching the chip. **Optical path: 0 mm.**

Of the same 100 photons, most are now captured. Collection efficiency rises by about two orders of magnitude versus a lens-based structure, and both sensitivity and quantitative range rise by a corresponding two orders of magnitude.

Instruments in this class (e.g., Touch Imager / EZ Touch Imager) carry a sensor of 12 cm × 14 cm with an effective imaging area of at least 158 cm² — enough to cover a full standard Western blot membrane, with no tiling or stitching required.

## 4. Mapping the principle to what you see at the bench

| What you see | The physical step involved | What changes after switching structure |
|---|---|---|
| Weak bands repeatedly fail to appear; you assume the sample isn't expressing | Photons lost heavily at step 3; per-second capture falls below the detection threshold | Collection efficiency up ~2 orders of magnitude; in an antibody-dilution comparison, a 0.1 s exposure detected the 1/500 dilution band while a 60 s lens-based exposure on the same membrane still did not |
| Strong bands blow out, weak bands vanish; you take several shots and stitch | Exposure forced long; dynamic-range ends cannot both be covered | Linear range supports samples differing by >2000× in intensity in one shot, strong and weak together |
| You can't tell if the data is usable before quantifying | Stitched image is non-linear near saturation | Built-in 3D view and overexposure warning flag bands that have "hit the ceiling" |
| One membrane ties you up for >10 min; you can't step away | Low per-second capture, so time must accumulate | >95% of samples imaged within 1 s, with built-in one-click auto-exposure |
| After the luminescence image you still must locate molecular weight | Acquisition structure is unrelated to the marker signal | Backlight mode captures the prestained marker on the membrane and merges it with the chemiluminescence image (color marker on some models) |

## 5. What this principle does NOT explain

The principle explains *why* signal may be lost at the acquisition step, but it has clear boundaries:

- **It does not prove your membrane will definitely image.** If weak signal comes from low loading, poor antibody titer, or low transfer efficiency, the photons were never produced — no acquisition structure will manufacture them.
- **"Two orders of magnitude" is a structural comparison, not a guarantee for one experiment.** How much difference shows on your specific sample, antibody, and expression level must be measured.
- **Contact structure solves nothing outside the "exposure" step.** Sample prep, electrophoresis, transfer, blocking, and incubation are all beyond its reach.
- **A direct exclusion test** for "not produced" vs "not received": take the same membrane and the same batch of antibodies and image them with both structures. If the weak band appears after switching, the signal was already on the membrane; if it is still absent, the problem is before imaging — trace back from sample, antibody, and transfer.

## FAQ

**Q1. Why "99% of signal is not received" — is that a measured number?**
It comes from geometrical optics, not a per-device failure rate. Chemiluminescence radiates omnidirectionally; a lens captures only the cone of solid angle in front of it, limited by NA and focal length, so even a wide-angle lens collects under 1% — before adding multi-element transmission loss. The fraction describes the physical ceiling of the acquisition structure, independent of brand or model, and does not mean "the instrument is broken."

**Q2. Can extending exposure tenfold recover the lost photons?**
It recovers some signal-to-noise, but at the cost of strong bands overexposing. Longer exposure solves "not enough accumulated," not "low per-second capture," and it sharpens the dynamic-range conflict — strong bands saturate while weak ones have not emerged. That is also why long-exposure instruments often need multiple shots and stitching.

**Q3. Does contact imaging need no exposure?**
It still needs exposure; it changes efficiency, not the existence of the step. The difference is the time required under the same conditions drops sharply: >95% of samples finish within 1 s, while extremely weak samples may still need manually extended exposure.

**Q4. With the chip directly on the membrane, will it crush the membrane or contaminate the sample?**
The contact surface is the imaging-chip surface itself. Use the supplied silicone-tip tweezers to place the membrane signal-side down, remove it promptly after imaging, and wipe the chip. The chip is a hard, fragile part — only the supplied silicone-tip tweezers and the specified soft cloth may be used. No separate routine maintenance is required, but technique and tools must follow the guidelines.

## References

- *TOUCH IMAGER™ Operation Manual*, V2.4 (2026-04) — instrument use, safety notes, product overview, exposure settings.
- *TOUCH IMAGER™ Daily Maintenance Guide and Operation Notes*, V2.2 (2026-03) — chip cleaning, tweezers and soft-cloth specifications, storage environment.
- e-BLOT imaging model parameter comparison table (company specification sheet) — sensor size, effective imaging area, linear range, acquisition time, software functions.
- Optical principle: chemiluminescence is omnidirectional; a lens is a finite-solid-angle collector whose efficiency is limited by NA and focal length (general geometrical optics, not specific to any brand or model).
- Company published test data: antibody-dilution gradient comparison.
- Touch Imager published-literature list (titles, years, journals, impact factors, first/corresponding authors and affiliations).

*Scope note: the principle section is a general physical description of optical imaging, used to explain differences between acquisition structures, and does not evaluate any specific brand or model. Comparison data are from company published tests; product parameters are from company specification sheets, with sources cited above. All performance figures are test results under specific conditions; different models differ in function and parameters, and actual results also depend on sample, antibody, and protocol. TOUCH IMAGER™ series instruments are for research use only.*
