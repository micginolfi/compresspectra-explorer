# Spectra Explorer

Interactive map of 17.450 JWST/NIRSpec PRISM spectra from the DAWN JWST Archive (DJA).
Each point is a spectrum. Similar spectra sit close together on the map.

**Link for the explorer:** https://micginolfi.github.io/compresspectra-explorer/

## How the map is made

1. Spectra are moved to a common rest-frame grid and normalised.
2. A PCA compresses each spectrum into 10 components (the embedding).
3. UMAP projects the embedding to 2-D for display.

Sample: DJA grade-3 PRISM spectra, S/N > 1 (sn50), one spectrum per source, excluding
spectra with large internal gaps.

## How to use it

**Map**
- Wheel: zoom. Drag: pan. Double-click: reset.
- Click a point to see its spectrum, redshift and catalogue information.
- Use the search box to find an object by name, ID or Paper I object number.

**Overlays**
- **Colour by z:** colours points by redshift.
- **LRD spec confirmed:** de Graaff+25 and our spectroscopically confirmed LRDs.
- **BLAGN:** broad-line AGN from Baccus+25 and Taylor+26.
- **True embedding neighbours:** see below.

**Spectrum**
- Choose the x scale (log or linear), frame (rest or observed), y quantity (f_lambda or f_nu)
  and y scale (linear or log).
- Default: rest-frame linear f_lambda against log wavelength.
- Black dots show the binned continuum with emission lines masked.
- Wheel: zoom in wavelength. Double-click: reset.

**Cutouts**
- RGB cutouts load from the DJA and need a connection. Spectra are stored in the page.

**H-band magnitude cut.** The slider in the top bar shows only spectra brighter than a chosen H-band AB magnitude (off by default). For each spectrum, H is computed from the PRISM spectrum itself by synthetic photometry: the flux density (µJy, DJA point-source slit-loss correction applied) is averaged over the 2MASS H filter, weighting each pixel by the filter transmission T, its width Δλ and 1/λ (photon-counting convention), ⟨f_ν⟩ = Σ f_ν T Δλ/λ / Σ T Δλ/λ, and converted to H = 23.9 − 2.5 log₁₀⟨f_ν⟩. Only valid pixels are used; H is undefined when they cover less than 80% of the filter weight or when ⟨f_ν⟩ ≤ 0, and such spectra are shown only when the cut is off. For compact sources the values agree with NIRCam F150W photometry to within a few hundredths of a magnitude (scatter ~0.3 mag); extended galaxies come out fainter because of slit losses.

## True embedding neighbours

Clicking an object draws lines to its 10 nearest objects in the full 10-D embedding.
These are its most similar spectra.

UMAP cannot keep all distances when it squeezes the embedding into 2-D. Long lines mean the
map has separated objects that are really close.

**Always trust the neighbours over distances on the map.**

## Limitations

- Fluxes are normalised, not absolute.
- The map is for exploration. Measure distances in the embedding, not on the map.
- A position near known LRDs does not make an object an LRD.
- Low-S/N spectra can look noisy, and negative fluxes do not appear on a log y-axis.
