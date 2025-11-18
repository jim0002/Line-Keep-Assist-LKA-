# Line Keep Assist (LKA) — Classical Computer Vision Pipeline

Implementation of a Line Keep Assist (LKA) function using video analysis of an ADAS front camera.  
The pipeline follows a classical computer vision approach and is designed to match typical LKA perception requirements: lane detection, lane geometry estimation, and simple control-related metrics.

---

## Overview

This project processes a driving video frame by frame to detect and track lane boundaries.  
From the detected lanes it estimates:

- Left and right lane positions
- Lateral offset of the ego vehicle from lane center (px and meters)
- Confidence values for each lane side
- Basic temporal stability metrics

These outputs form the perception backbone for a Line Keep Assist system.

---

## Key Features

- **Lane boundary detection** using HLS color and Sobel-x gradient thresholds  
- **Bird’s-eye view (IPM / perspective warp)** for more stable lane geometry  
- **Histogram-based sliding window search** to collect lane pixels  
- **2nd-order polynomial fitting** for left and right lane curves  
- **Lightweight temporal smoothing** of polynomial coefficients and confidence  
- **Per-frame confidence estimation** and lateral offset in pixels and meters  
- **Real-time HUD overlay** with lane polylines, offset and confidence  
- **CSV logging** of all frame-wise metrics for later evaluation

---

## Pipeline Summary

| Step | Description |
|------|------------|
| **1. Preprocessing** | Apply HLS and Sobel-x thresholds to emphasize lane markings. |
| **2. Perspective Transform** | Warp the road region into a bird’s-eye (top-down) view using a fixed homography. |
| **3. Lane Detection** | Use a bottom-half histogram to find lane bases and run sliding windows upwards. |
| **4. Polynomial Fit** | Fit 2nd-order polynomials to left and right lane pixels in the warped space. |
| **5. Temporal Smoothing** | Exponentially smooth polynomial coefficients and confidence across frames. |
| **6. Metrics \& Alerts** | Compute confidence, lateral offset and simple stability indicators. |
| **7. Visualization \& Output** | Render annotated frames with HUD and log metrics into a CSV file. |

---

## Outputs

After running the main notebook / script, you obtain:

| File | Description |
|------|------------|
| `annotated_video.mp4` | Final video with lane overlays and HUD (Left/Right detection, confidence, lateral offset). |
| `per_frame_polyfit.csv` | Per-frame metrics: lane detection flags, confidence scores, lateral offset, etc. |

---

## Usage (Colab / Local)

1. Clone the repository:
   ```bash
   git clone https://github.com/jim0002/Line-Keep-Assist-LKA-.git
   cd Line-Keep-Assist-LKA-
