# DroneZ Submission Checklist

| Item | Command | Expected Output | Current Status |
| --- | --- | --- | --- |
| Editable install | `python -m pip install -e .` | Editable package installs successfully | `PASS` |
| Local tests | `pytest -q` | All tests pass | `PASS` |
| Evaluation artifacts | `python scripts/evaluate_policies.py` | Regenerates `artifacts/results/policy_comparison.json` and `.csv` | `PASS` |
| Demo traces | `python scripts/generate_demo_trace.py --task demo --policy all` | Regenerates all four demo trace files | `PASS` |
| Plot generation | `python scripts/generate_plots.py` | Regenerates the three comparison plots | `PASS` |
| Smoke training | `python scripts/train_grpo.py --mode smoke` | Writes `artifacts/results/training_smoke_metrics.json` | `PASS` |
| Dry-run training prep | `python scripts/train_grpo.py --mode dry-run` | Writes `artifacts/training/*.json` without claiming training happened | `PASS` |
| Colab entrypoint prep | `python scripts/train_grpo_colab.py --dry-run --model Qwen/Qwen2.5-0.5B-Instruct --tasks easy,medium,demo --output-dir artifacts/training` | Writes dry-run training artifacts through the Colab entrypoint | `PASS` |
| OpenEnv validation | `openenv validate` | Ready for multi-mode deployment | `PASS` |
| Local server endpoints | `python -m uvicorn server.app:app --host 127.0.0.1 --port 8000` plus `/health`, `/tasks`, `/reset`, `/state`, `/step` curls | Server binds and serves the OpenEnv-compatible API | `PASS` |
| Docker build and run | `docker build -t dronez .` plus `docker run --rm -p 8000:7860 dronez` | Image builds, container runs, and local `/health`, `/tasks`, `/reset`, `/state`, `/step` work | `PASS` |
| Real GRPO run | `python scripts/train_grpo_colab.py --model Qwen/Qwen2.5-0.5B-Instruct --tasks easy,medium,demo --output-dir artifacts/training` on Colab / hackathon GPU | Real `eval_before`, `eval_after`, and training metrics | `NOT RUN` |
| HF Space deployment | Follow `HF_SPACE_DEPLOYMENT.md` | Live public Space with `/health`, `/tasks`, `/reset`, `/state`, `/docs`, `/demo/index.html` | `PASS` |
| HF link in README | Edit `README.md` Submission Links section | Real Space URL added | `PASS` |
| Video / blog / slides links | Edit `README.md` Submission Links section | Real supporting links added | `TODO` |
| Colab link in README | Edit `README.md` Submission Links section | Public Colab URL added | `PASS` |
| README review | Open `README.md` | Final judge-facing story is correct and honest | `PASS` |
| Pitch review | Open `PITCH.md` | Team stage answers are rehearsed | `PASS` |
| Junk-file cleanup | `git status --short` | No cache junk or accidental duplicate files | `PASS` |
| Clean git status before submission | `git status --short` | No pending local changes | `PASS` |

## Current Blocked Details

- Real GRPO / TRL / Unsloth training remains `NOT RUN`; run it in Colab or GPU compute before claiming trained-model improvement.
- Video/slides and public blog links remain `TODO`; README currently points to local `BLOG.md` and has placeholders for video/slides.

## Final Human Actions Before Submission

1. Run the real GRPO / TRL job on Colab or hackathon compute if time allows.
2. Replace video/slides and public blog links in README once they exist.
3. Rehearse `FINAL_STAGE_SCRIPT.md` with the live Space, docs, demo UI, and reward plots.
4. Submit the HF Space URL: `https://huggingface.co/spaces/Krishna2521/dronez-openenv`.
