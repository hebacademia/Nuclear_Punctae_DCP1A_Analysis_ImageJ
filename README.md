

# Assignment 1 - ImageJ Particle Counter
## DCP1A P-body Particle Counting Protocol

---

### Introduction

DCP1A (Decapping mRNA 1A) is a core component of cytoplasmic processing bodies (P-bodies) — discrete, membraneless ribonucleoprotein granules found in the cytoplasm of eukaryotic cells. The primary role of DCP1A is to facilitate mRNA decapping, the removal of the 5' protective cap from messenger RNA molecules, committing them to degradation. This process is critical for post-transcriptional gene regulation, influencing cell proliferation, stress response, and RNA quality control. Under fluorescence microscopy, DCP1A appears as bright white cytoplasmic punctae, and quantification of these punctae using ImageJ provides insight into P-body number and distribution under varying cellular conditions.

---

### Image Information
**Protein:** DCP1A (Decapping mRNA 1A)

**Source:** OpenCell database (https://opencell.sf.czbiohub.org/)

**Raw Image link:**  https://opencell.sf.czbiohub.org/target/837

**Image format:** TIF

**What is being counted:** DCP1A-positive P-bodies — discrete cytoplasmic ribonucleoprotein particles, not cells

---

### STEP 1 : Open the Image
I opened the DCP1A image by navigating to **File → Open** and selecting the TIF file. Upon opening, the image displayed bright white P-body punctae scattered in the cytoplasm surrounding blue DAPI-stained nuclei on a black background. These bright white dots represent the particles that were counted throughout this analysis.

---

### STEP 2 : Subtract Background
I navigated to **Process → Subtract Background** and set the Rolling ball radius to **6.0**, ensuring that **"Light background" was unchecked** given the black background of the image.

This step mathematically removes uneven background illumination and low-level background haze from the image. A rolling ball of radius 6.0 pixels rolls across the image surface and subtracts any intensity not attributable to a discrete bright structure, allowing the white P-body dots to stand out more cleanly against the dark background in preparation for accurate thresholding in subsequent steps.

---

### STEP 3 : Convert to 8-bit
I converted the image to 8-bit grayscale by navigating to **Image → Type → 8-bit**.

This step converted the image from a 3-channel RGB colour image into a single-channel 8-bit grayscale image, where each pixel carries a brightness value between 0 (pure black) and 255 (pure white). As a consequence of this conversion, the blue DAPI nuclear signal - comparatively dim in grayscale terms - largely disappeared, while the bright white DCP1A P-body dots remained clearly visible as the dominant signal in the image. This format is required for thresholding and particle analysis in ImageJ.

---

### STEP 4 : Adjust Threshold
I navigated to **Image → Adjust → Threshold** and set the minimum threshold value to **115** and the maximum threshold value to **255**, after which I clicked **Apply** and closed the threshold window.

The threshold defines which pixels are classified as particles and which are classified as background. Pixels with brightness values between 115 and 255 were designated as particle signal, while all values below 115 were treated as background. Setting the minimum threshold at 115 ensured that only genuinely bright P-body dots were selected, excluding any residual dim signal remaining from the blue nuclei after 8-bit conversion. Following the application of the threshold, the image was converted into a binary black and white image in which P-body dots appeared as solid black dots on a white background - the format required for downstream particle analysis.



**Note on Binary Processing Steps:**

Upon visual inspection of the binary image obtained after thresholding, the DCP1A P-body dots appeared as solid, well-separated black dots on a white background. Given this observation, the binary processing steps - Fill Holes, Convert to Mask, and Watershed - were deemed unnecessary and were not performed. Fill Holes is required only when particles appear as hollow rings, Convert to Mask is a standardisation step applicable only when binary processing is carried out, and Watershed is required only when particles are touching or clustered together. Since none of these conditions were observed in the thresholded image, the analysis proceeded directly to setting measurements.

---

### STEP 5 : Set Measurements
I navigated to **Analyze → Set Measurements** and enabled the following parameters: **Area, Centroid, Perimeter, Shape descriptors** and **Display label**, then clicked **OK**.

This step defined the quantitative data that ImageJ would record for each detected particle. Area provided the size of each particle in pixels², Centroid recorded the central coordinate of each particle, Perimeter measured the boundary length, and Shape descriptors provided the circularity value - a numerical confirmation of how round each particle is. Together, these parameters produced a comprehensive quantitative profile for every P-body identified in the analysis.

---

### STEP 6 : Analyze Particles
I navigated to **Analyze → Analyze Particles** and entered the following parameters:

- **Size (pixel²):** 10 - 80
- **Circularity:** 0.75 - 1.00
- **Show:** Outlines
- **Checked:** Display results, Clear results, Summarize

I then clicked **OK** to execute the analysis.

The **size filter of 10–80 pixels²** was applied to exclude single noise pixels below the size of a real P-body (under 10 pixels²) as well as large debris or artefacts exceeding the expected size of a P-body (above 80 pixels²), thereby restricting detection to particles of biologically relevant dimensions. The **circularity filter of 0.75-1.00** was applied on the basis that DCP1A P-bodies are morphologically round punctae - any elongated or irregularly shaped artefacts were consequently rejected by this filter. Selecting **Outlines** generated a new image in which every counted particle was assigned a number, enabling visual verification of the final count.

Three outputs were automatically generated upon completion: a **Results table** listing each individual particle alongside its full set of measurements, 
a **Summary table** reporting the total particle count, and 
an **Outlines image** displaying a numbered outline over each detected particle.

---

### STEP 7 — Save the Results Table
I saved the Results table by navigating to **File → Save As** within the Results table window, saving the file as `DCP1A_particle_results.csv` to the designated GitHub results folder. The Summary table was saved in the same manner as `DCP1A_summary.csv`.

---

