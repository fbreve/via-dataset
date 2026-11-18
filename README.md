# VIA Dataset — Visual Impairment Aid: Clear and Non-Clear Paths

**342 labeled photographs of pathways and obstacles** for research into computer vision and assistive navigation, introduced in the IJCNN 2020 paper by Fabricio Aparecido Breve and Carlos Norberto Fischer.

<details>
<summary>Quick facts</summary>

| Property | Value |
| --- | --- |
| Task | Binary image classification |
| Images | 342 JPEG photographs |
| Classes | `clear`: 175; `nonclear`: 167 |
| Image resolution | 750 × 1000 pixels, as described in the paper |
| Source | Smartphone photographs taken by Fabricio Aparecido Breve |
| License | [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE) |
| Companion code | [fbreve/via-py](https://github.com/fbreve/via-py) |
| Dataset details | [DATASET_CARD.md](DATASET_CARD.md) |

</details>

## Images and labels

The dataset is stored in [`images/`](images/) as 342 JPEG files:

| Label | Interpretation | Images | Filenames |
| --- | --- | ---: | --- |
| `clear` | Clear path ahead | 175 | `clear.000.jpg` – `clear.174.jpg` |
| `nonclear` | Path containing an obstacle | 167 | `nonclear.000.jpg` – `nonclear.166.jpg` |

The class label is the **filename prefix before the first period**, not a separate CSV annotation. There are no missing indices in either sequence, and there are no official train/test splits or instance-level obstacle annotations.

The images were acquired from a smartphone held at approximately chest height and tilted downward, then resized to 750 × 1000 pixels. The published collection includes indoor and outdoor scenes, variable lighting and surface conditions, and several obstacle types. The photographer confirms that the pictures were taken by him and contain no people.

See [DATASET_CARD.md](DATASET_CARD.md) for acquisition details, limitations, intended uses, licensing scope, and provenance.

## Use with the research implementation

The companion [`via-py`](https://github.com/fbreve/via-py) repository contains the associated Python experiments and expects the dataset and code repositories to be **sibling directories**:

```text
research/
├── via-dataset/
│   └── images/
│       ├── clear.000.jpg
│       ├── ...
│       └── nonclear.166.jpg
└── via-py/
```

The scripts in `via-py` look for the photographs under `../via-dataset/images/`. In the main scripts, the labels are mapped as `clear → 0` and `nonclear → 1`.

For new analyses, use a deterministic filename order and record the train/test split and random seeds. **The dataset repository itself does not include the training code or reproduce the numerical results of the publications.** Historical experimental results and software-specific requirements belong to `via-py` and the papers.

## Publications and citation

The dataset was introduced in the following paper. **Please cite this publication** when using the dataset for research:

> Fabricio Aparecido Breve and Carlos Norberto Fischer. **Visually Impaired Aid using Convolutional Neural Networks, Transfer Learning, and Particle Competition and Cooperation.** *2020 International Joint Conference on Neural Networks (IJCNN)*, 2020.
>
> [DOI](https://doi.org/10.1109/IJCNN48605.2020.9207606) · [arXiv](https://arxiv.org/abs/2005.04473) · [Author-hosted manuscript](https://www.fabriciobreve.com/artigos/2020/wcci2020.pdf)

```bibtex
@inproceedings{breve2020visually,
  author    = {Breve, Fabricio Aparecido and Fischer, Carlos Norberto},
  title     = {Visually Impaired Aid using Convolutional Neural Networks,
               Transfer Learning, and Particle Competition and Cooperation},
  booktitle = {2020 International Joint Conference on Neural Networks (IJCNN)},
  year      = {2020},
  doi       = {10.1109/IJCNN48605.2020.9207606}
}
```

The same dataset was subsequently used in a further study:

> Fabricio Aparecido Breve. **Convolutional Neural Networks and Ensembles for Visually Impaired Aid.** *Computational Science and Its Applications — ICCSA 2023*, 2023.
>
> [DOI](https://doi.org/10.1007/978-3-031-36805-9_34) · [Author-hosted manuscript](https://www.fabriciobreve.com/artigos/2023/iccsa2023.pdf)

```bibtex
@incollection{breve2023convolutional,
  author    = {Breve, Fabricio Aparecido},
  title     = {Convolutional Neural Networks and Ensembles for Visually Impaired Aid},
  booktitle = {Computational Science and Its Applications -- ICCSA 2023},
  publisher = {Springer},
  year      = {2023},
  doi       = {10.1007/978-3-031-36805-9_34}
}
```

GitHub's **Cite this repository** option uses [`CITATION.cff`](CITATION.cff), with the IJCNN 2020 paper as the preferred reference.

## License and attribution

**The photographs and their dataset annotations are licensed under [CC BY 4.0](LICENSE).**

Photographer and copyright holder: **Fabricio Aparecido Breve**.

You may copy, share, and adapt the photographs for research or commercial purposes, provided you comply with CC BY 4.0, including appropriate attribution, a license link, and an indication of modifications when relevant. A suggested attribution is:

> VIA dataset photographs by Fabricio Aparecido Breve — https://github.com/fbreve/via-dataset — CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/).

Citing the academic paper is **requested** but is **not an additional condition of the CC BY 4.0 license**. The photographs' CC BY license is distinct from the [Apache 2.0 software license in `via-py`](https://github.com/fbreve/via-py/blob/master/LICENSE).

## Dataset integrity

[`IMAGE_MANIFEST.csv`](IMAGE_MANIFEST.csv) records for each photograph:

- Relative path and the class taken from the filename;
- File size in bytes;
- **Git blob SHA-1**, an object identifier used by Git.

All **342 image objects remain identical to the earliest complete Git commit** (February 3, 2020); they were subsequently reorganized into the `images/` folder without modification.

You can verify an individual file from a checked-out repository:

```bash
git hash-object images/clear.000.jpg
```

Compare the output with the `git_blob_sha1` column in the manifest. This Git object hash is **not the ordinary SHA-1 hash of the JPEG bytes**, nor a SHA-256 checksum.

## Limitations and safety

This is a small experimental dataset, **not a validated obstacle-detection or navigation product**. Binary labels do not specify obstacle distance, severity, or exact location, and measured classification accuracy on this dataset alone does not establish real-world safety. See the [dataset card](DATASET_CARD.md) and the original articles for the intended experimental context.
