# FineGrade: A Rule-Consistent Scoring Framework for Fine-Grained Action Quality Assessment

This repository hosts the **dataset release** for **FineGym-AQA**, a fine-grained action quality assessment benchmark built on top of **FineGym**.

Extending FineGym’s hierarchical **event–set–element** annotations, FineGym-AQA augments routine instances with judge-aligned scoring signals, including **Difficulty (D)**, **Execution (E)**, **Neutral Deduction (ND)**, and **Total (T)**, together with fine-grained temporal segments, element codes, and difficulty values (DV) when available.

> **Current status**
> 
> This repository currently mainly contains:
> - score-augmented annotation **JSON** files
> - original competition **result book PDFs**
> 
> Training / inference code, pretrained models, and feature extraction scripts are **not included yet** and will be released later.

## Highlights

- Built upon the hierarchical annotation design of **FineGym**.
- Covers four artistic gymnastics apparatus:
  - **VT**: Vault
  - **FX**: Floor Exercise
  - **BB**: Balance Beam
  - **UB**: Uneven Bars
- Provides routine-level judging signals: **D / E / ND / T**.


## Dataset Summary

FineGym-AQA focuses on four apparatus and contains **3,516 score-augmented routine instances**. It inherits FineGym’s hierarchical semantics with **15 set classes** and **530 element classes**.

| Event | Score-augmented instances |
|------|---------------------------:|
| VT   | 1202 |
| FX   | 661  |
| BB   | 795  |
| UB   | 858  |
| Total| 3516 |



## Annotation Format

Each source video is indexed by a video ID. Event clips are stored under keys such as `E_000133_000140`.

A typical event entry may contain:

- `event`: apparatus ID
  - `1`: VT
  - `2`: FX
  - `3`: BB
  - `4`: UB
- `timestamps`: clip-level timestamps in the source video
- `segments`: fine-grained element/action segments
- `score`: routine-level scores (`diff`, `execution`, `nd`, `total`)
- `name` / `number`: athlete metadata when available

### Example

```json
{
  "0jqn1vxdhls": {
    "E_000133_000140": {
      "event": 1,
      "timestamps": [[133.56, 140.68]],
      "name": "Jordyn Wieber",
      "number": "8",
      "score": {
        "diff": 6.5,
        "execution": 9.6,
        "nd": 0.0,
        "total": 16.1
      },
      "segments": {
        "A_0000_0007": {
          "stages": 3,
          "timestamps": [[0.04, 3.49], [3.49, 4.70], [4.70, 7.11]],
          "code": "6.50"
        }
      }
    }
  }
}
```

For longer routines (especially **FX / BB / UB**), `segments` may contain multiple element instances. Each segment may include:

- local timestamps within the event clip
- element `code`
- optional element difficulty value `dv`

## About the result books

The raw **result book PDFs** are kept in this repository for transparency and reproducibility. They are the original competition documents used during score alignment and manual verification.

## Citation

If you find this repository useful, please consider citing **FineGym**. A citation entry for **FineGrade / FineGym-AQA** will be added after the paper is publicly released.

```bibtex
@inproceedings{shao2020finegym,
  title={FineGym: A Hierarchical Video Dataset for Fine-grained Action Understanding},
  author={Shao, Dian and Zhao, Yue and Dai, Bo and Lin, Dahua},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  year={2020}
}
```

## Acknowledgment

This project is built upon **FineGym** and follows its hierarchical annotation philosophy for fine-grained gymnastics understanding.
