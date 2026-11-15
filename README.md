# Mixed flocks in open space

Code for the paper *Segregation with cohesion: a quantum-inspired perceptual model of mixed flocks in open space*, by Mayank Chaurasiya, Ayush Agrawal, Chirayush Mohanty and Laxmidhar Behera (Indian Institute of Technology Mandi and Indian Institute of Technology Kanpur).

Archived on Zenodo, with the output of every run and the video: DOI to be added.

Agents of three kinds move at constant speed in an open plane. Each agent perceives six partners, chosen in proportion to how similar they are to it, and adds their headings and bearings as amplitudes in one superposed state. The bearing of a partner of another kind enters with a minus sign. The agent draws its next heading from the squared perceptual state, which carries memory of earlier steps (Born rule). With these two ingredients the kinds segregate into single-kind clusters while the flock stays together.

## What is here

| File | What it does |
|---|---|
| `paper.ipynb` | Every simulation, table and figure of the paper, in order. Start here. |
| `flock_model.py` | The model as a Python module (the same code as Sections 1–4 of the notebook), used by the scripts in `checks/`. |
| `checks/lopsided_draw.py` | How much the minus sign shifts the draw away from the other kind. |
| `checks/subgroup_gaps.py` | Whether the subgroups drift apart over time (signed vector sum, vector sum with other kinds' bearings ignored, full model). |
| `checks/measures_k.py` | The mixing entropy for 5, 10, 20 and 40 neighbours, and cohesion for other link distances. |
| `checks/visual_cone.py` | How wide the visual cone must be (90° to 330°; Table 5). |
| `checks/vector_tuning.py` | The vector sums with a weaker minus sign and other weights of headings (ESM table S1). |
| `checks/couzin_identity.py` | The zonal model of Couzin et al. (2002) in open space with the attraction to other kinds scaled by c (ESM table S2). |
| `checks/distance_decay.py` | The full model when the weight of a partner falls with its distance (Section 4). |
| `checks/appendix_math.py` | The closed forms of the overlaps against numerical integrals, and the worked example (ESM appendices B and C). |

## Install

Python 3.9 or newer.

```
pip install -r requirements.txt
```

`ffmpeg` is needed only for the video in the last section of the notebook.

## Run

**Check first.** In `paper.ipynb`, Section 1, set `QUICK_TEST = True` and run all cells. This uses tiny flocks and short runs and checks that every cell works in a few minutes. The numbers it prints are not the paper's.

**Full run.** Set `QUICK_TEST = False`, set `N_JOBS` to the number of CPU cores to use, and run all cells. All tables, figures and data go to `output/`.

One run of 5,000 steps takes about 25 s for 240 agents, 80 s for 480 and 4 min for 960, on one core. The whole notebook is about 40 core-hours, so about 4 hours on 10 cores. Every run is saved as soon as it finishes, under a key made from all of its parameters, so the notebook can be stopped and restarted and only what is missing is computed. Section 7 (the large flocks) is about a quarter of the time; to shorten it, remove the entry `960` from `LIMIT_PLAN`.

**Checks.** From the repository folder:

```
python checks/appendix_math.py        # a few seconds
python checks/lopsided_draw.py 60     # a few minutes
python checks/subgroup_gaps.py        # about 10 minutes on 4 cores
python checks/measures_k.py           # about 10 minutes on 4 cores
python checks/visual_cone.py          # about 4.5 hours on 4 cores
python checks/vector_tuning.py        # about 6 hours on 4 cores
python checks/couzin_identity.py      # about 1.5 hours on 4 cores
python checks/distance_decay.py       # about 1 hour on 4 cores
```

Set the number of cores with `N_JOBS`, for example `N_JOBS=8 python checks/subgroup_gaps.py`.

## Where each result comes from

| Paper | Notebook section or script |
|---|---|
| Figures 1–3, ESM appendix C (one decision worked through) | Section 14 |
| Table 2, Figures 4 and 5 (the model and its controls) | Section 5 |
| Table 3 (decision rules) and its tests | Section 6 |
| Table 4 (headings and bearings), ESM table S8 (960 agents, 15,000 steps) | Section 11 |
| Figure 6, ESM table S7 (range of sight) | Section 7 |
| Figure 7 (attention to other kinds) | Section 8 |
| Table 5 (visual cone) | Section 16 (or `checks/visual_cone.py`) |
| ESM figure S1 (noise) | Section 9 |
| ESM figure S2 (single quantities changed) | Section 10 |
| ESM figure S3 (long runs) | Section 13 |
| ESM figure S4, appendix E (order seen from perceptual space) | Section 12 |
| ESM appendix B (Vicsek-like limit) | Section 15 |
| ESM table S1 (vector sums at other settings) | Section 17 (or `checks/vector_tuning.py`) |
| ESM table S2 (zonal model with identity) | Section 18 (or `checks/couzin_identity.py`) |
| Partners weighted by distance (Section 4) | Section 19 (or `checks/distance_decay.py`) |
| Every number quoted in the text | Section 20, `output/numbers_for_manuscript.txt` |
| Video of the three cases | Section 22 |

## Seeds

Tables 2, 3 and 4 use seeds 3000–3029 (the same 30 starting states for every case). The sweeps of attention, noise and single quantities use seeds 2000–2029, the cone, vector-sum, zonal-model and distance checks use 3000–3029, and the range-of-sight runs start at 4000. All seeds are set in Section 1 of the notebook.

## Citation

If you use this code, please cite the paper (reference to be added on publication).

## Licence

MIT, see `LICENSE`.
