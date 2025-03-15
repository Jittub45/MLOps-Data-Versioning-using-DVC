# MLOps Complete ML Pipeline

Introduction
This project demonstrates an end-to-end ML pipeline incorporating DVC for experiment tracking and data versioning with AWS S3 as remote storage. It includes structured steps for building and managing an ML pipeline efficiently.

Tech Stack & Tools Used
- Languages: Python
- ML Tools: Scikit-learn, NumPy, Pandas
- Experiment Tracking: MLflow, DVCLive
- Version Control: DVC, GitHub
- Remote Storage: AWS S3, DagsHub
- Deployment: (Planned for future work)

Project Setup

1. Building the Pipeline
    1. Create a GitHub repository and clone it locally.
    2. Add the `src` folder with all components and run them individually.
    3. Add `data`, `models`, and `reports` directories to `.gitignore`.
    4. Use `git add .`, commit, and push the code to the repository.

2. Setting Up DVC Pipeline (Without Params)
    1. Create `dvc.yaml` and define pipeline stages.
    2. Run `dvc init`, followed by `dvc repro` to test the pipeline automation.
    3. Check pipeline structure using `dvc dag`.
    4. Commit and push changes using Git.

3. Setting Up DVC Pipeline (With Params)
    1. Add a `params.yaml` file.
    2. Configure the required parameters.
    3. Run `dvc repro` to integrate parameter tracking.
    4. Commit and push changes using Git.

4. Experimenting with DVC
    1. Install `dvclive` using `pip install dvclive`.
    2. Implement the DVCLive tracking code.
    3. Run `dvc exp run` to track experiments.
    4. View experiments using `dvc exp show` or via the DVC VSCode extension.
    5. Use `dvc exp remove {exp-name}` to delete an experiment and `dvc exp apply {exp-name}` to revert to a previous experiment.
    6. Modify parameters and re-run experiments.
    7. Commit and push all changes.

5. Adding Remote S3 Storage to DVC
    1. Login to AWS and create an IAM user.
    2. Create an S3 bucket with a unique name.
    3. Install dependencies: `pip install dvc[s3]` and `pip install awscli`.
    4. Configure AWS credentials using `aws configure`.
    5. Add remote storage: `dvc remote add -d dvcstore s3://bucketname`.
    6. Use `dvc commit` and `dvc push` to store experimental results.
    7. Commit and push changes to GitHub.

Parameters Setup (`params.yaml`)
```python
import yaml

def load_params(params_path: str) -> dict:
    """Load parameters from a YAML file."""
    try:
        with open(params_path, 'r') as file:
            params = yaml.safe_load(file)
        return params
    except Exception as e:
        raise e

# Usage Example
params = load_params('params.yaml')
test_size = params['data_ingestion']['test_size']
max_features = params['feature_engineering']['max_features']
model_params = params['model_building']
```

DVCLive Code Block
```python
from dvclive import Live
import yaml

with Live(save_dvc_exp=True) as live:
    live.log_metric('accuracy', accuracy_score(y_test, y_pred))
    live.log_metric('precision', precision_score(y_test, y_pred))
    live.log_metric('recall', recall_score(y_test, y_pred))
    live.log_params(params)
```

Contact
For any queries, reach out via:
- GitHub: [Jittub45](https://github.com/Jittub45)
- Email: [jitendrakumaryadav2003@gmail.com]

Conclusion
This project serves as a foundational implementation of MLOps, integrating version control, experiment tracking, and cloud storage for ML pipelines. Future enhancements will focus on deployment strategies and automated model retraining.

