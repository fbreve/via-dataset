# Dataset card — VIA (Visually Impaired Aid)

## Overview

**VIA** is a small, two-class image-classification dataset introduced by Fabricio Aparecido Breve and Carlos Norberto Fischer in their 2020 IJCNN paper on visually impaired aid. The same dataset was later used for the CNN and ensemble experiments reported by Breve in ICCSA 2023.

- **Dataset repository:** https://github.com/fbreve/via-dataset
- **Implementation and experimental results:** https://github.com/fbreve/via-py
- **Primary publication:** https://doi.org/10.1109/IJCNN48605.2020.9207606
- **Follow-up publication:** https://doi.org/10.1007/978-3-031-36805-9_34
- **License:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE)
- **Photographer:** Fabricio Aparecido Breve

## Composition and labels

| Filename prefix | Published meaning | Count | Numeric encoding used in `via-py` |
| --- | --- | ---: | ---: |
| `clear` | A clear path, without an obstacle in the path of travel | 175 | 0 |
| `nonclear` | A non-clear path, with a potential obstacle | 167 | 1 |
| **Total** | | **342** | |

All images are JPEG files inside the top-level `images/` folder:

- `images/clear.000.jpg` through `images/clear.174.jpg`
- `images/nonclear.000.jpg` through `images/nonclear.166.jpg`

No sequence numbers are missing. These are **image-level binary class labels**; the repository contains no bounding boxes, depth measurements, segmentation masks, or obstacle coordinates.

The repository holds **342 images** totaling **154,225,141 bytes** of JPEG file content, as measured from the Git object tree. The image files have been preserved unchanged since the original February 2020 commit; they were moved into `images/` in March 2020 without changing their Git blobs.

## Acquisition and image characteristics

As described in the publications, photographs were collected using a smartphone camera at approximately chest height, aimed forward and angled down approximately 30–60 degrees to include several meters of the path ahead. Images were resized to **750 × 1000 pixels** for the released dataset.

The collection includes indoor and outdoor scenes, different floor and illumination conditions (including wet/dry surfaces and natural/artificial lighting), and obstacles such as stairs, trees, holes, animals, and traffic cones.

The photographer confirms that he took the pictures and that **no people appear in the released photographs**.

Details not supplied by the repository include the exact phone model, individual acquisition dates, geolocation metadata, and a per-image obstacle taxonomy. These should not be inferred from filenames.

## Intended use

Research and education involving obstacle-aware scene classification, transfer learning, compact CNNs, and semi-supervised image-classification methods.

The dataset was collected as a **research benchmark**. Its relatively small size, limited geographic and environmental coverage, and image-only binary labels mean that performance on it does **not** demonstrate reliable real-world navigation or safety. Do not rely on an image classifier trained solely on this collection as a standalone assistive navigation system.

## Splits and reproducibility

There are **no official train/validation/test split files** in this repository. Experimental splitting and validation belong to the cited papers and to their associated scripts. Do not infer an official split from filename sequence or Git listing order.

The companion `via-py` repository expects this structure if both repositories are checked out as siblings:

```text
research/
├── via-dataset/
│   └── images/
│       ├── clear.000.jpg
│       └── nonclear.000.jpg
└── via-py/
```

The relevant `via-py` scripts read from `../via-dataset/images/`; their label parsing uses the filename prefix before the first period. For new analyses, use a deterministic file order and record the selected sample IDs/splits. Do not assume that changing file order reproduces historical random splits exactly.

## Integrity and provenance

[`IMAGE_MANIFEST.csv`](IMAGE_MANIFEST.csv) lists the **relative path**, **class**, **size in bytes**, and **Git blob SHA-1** for all 342 images. A Git blob SHA-1 is computed over the bytes prefixed with a Git object header; it is **not** the ordinary SHA-1 of a JPEG file.

For an image in a Git checkout, compare the expected manifest field to the result of:

```bash
git hash-object images/clear.000.jpg
```

All original image blobs were also cross-checked against the earliest complete commit (`46329758dbda818a814f02d18a9317225d2b2fa1`, February 3, 2020). The only later structural image change was relocation to the `images/` directory.

## Ethics, limitations, and license scope

These photos were supplied by their photographer, Fabricio Aparecido Breve, for publication under CC BY 4.0. According to the photographer, no people appear in the images. No personal information or personally identifying annotations are distributed with the dataset.

The CC BY 4.0 license permits sharing and adaptation, including commercial use, subject to attribution and the other license terms. Refer to [LICENSE](LICENSE) and the [official legal code](https://creativecommons.org/licenses/by/4.0/legalcode).

The license for the photographs and accompanying dataset annotations is **separate** from the software license applicable to the `via-py` repository. Research papers and other external material retain their respective rights.

## References

**Primary (dataset introduction)**

Breve, Fabricio Aparecido, and Carlos Norberto Fischer. *Visually Impaired Aid using Convolutional Neural Networks, Transfer Learning, and Particle Competition and Cooperation.* IJCNN 2020. https://doi.org/10.1109/IJCNN48605.2020.9207606

**Follow-up application**

Breve, Fabricio Aparecido. *Convolutional Neural Networks and Ensembles for Visually Impaired Aid.* ICCSA 2023. https://doi.org/10.1007/978-3-031-36805-9_34
