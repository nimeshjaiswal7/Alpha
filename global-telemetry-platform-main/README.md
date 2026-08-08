# Global Telemetry Platform — Architecting and Implementing a Resilient Global Telemetry Platform

A PySpark 3.5.7 coursework project that implements a batch analytics pipeline for a global logistics fleet. The scenario models 500,000 vehicles continuously emitting telemetry — engine temperature, speed, GPS coordinates, battery efficiency, distance travelled, timestamps, vehicle IDs, and vehicle models — at a scale that demands distributed processing, fault tolerance, and deliberate handling of data skew. The graded notebook walks through the full assignment arc: system architecture and data paradigms (Modules 1–2), MapReduce and Spark theory, PySpark transformations and aggregations, salting for 1000× skew, RDD lineage and checkpointing, and advanced execution mechanics including lazy evaluation, DAG stages, data locality, and the liability of lineage.

## Project Structure

```
pyspark-dev/
├── notebooks/          # GradedAssignment.ipynb — main deliverable
├── src/                # Reusable Python modules (reserved)
├── diagrams/           # Architecture diagrams (reserved)
├── data/               # Synthetic telemetry CSV (gitignored)
├── checkpoints/        # Spark checkpoint files (gitignored)
├── output/             # Generated charts and job output (gitignored)
├── scripts/            # Notebook maintenance utilities
├── requirements.txt
└── .gitignore
```

## Setup

The development environment (WSL2, Python 3.12, Java 17, PySpark 3.5.7) is already installed and verified. To recreate the virtual environment on another machine:

```bash
cd pyspark-dev
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Running the Notebook Locally

Launch Jupyter from the project root or the `notebooks/` directory:

```bash
source .venv/bin/activate
jupyter notebook notebooks/GradedAssignment.ipynb
```

Run **Kernel → Restart & Run All**. The bootstrap cell auto-detects the environment via a `dbutils` probe and prints `Running on WSL2 local | BASE_DIR = ...` when running locally. No manual path edits are required.

## Azure Databricks Portability

The notebook is written to run on Azure Databricks **without modification**. When `dbutils` is present, the bootstrap switches `BASE_DIR` to a Unity Catalog Volume path (`/Volumes/workspace/telemetry/telemetryplatform`) and uses the cluster-managed SparkSession. Upload the notebook, data, and volume layout in Phase 2 — no code changes needed.
