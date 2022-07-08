# Machine Learning Template

## Repository Structure

```
├── Makefile
├── README.md
├── config
│   └── environment.yaml
├── data
│   ├── iterim
│   ├── processed
│   └── raw
├── notebooks
├── requirements.txt
├── saved
│   ├── figures
│   └── models
├── scripts
│   ├── eval.py
│   ├── process.py
│   └── train.py
└── src
    ├── __init__.py
    ├── model
    │   └── __init__.py
    ├── test
    └── utils
```

- The `Makefile` should be used to setup the repository (ex. install required OS libraries) or to save complex commands/workflows such as training or running experiments with many command line arguments.

- The `config` folder is versioned using DVC and should include configuration files related to your environment or experiments.

- The `data` folder is versioned using DVC and includes subfolders for `interim`, `raw`, and `processed` data.

- The `notebooks` folder should be used for data exploration or in other situations where data visualization may be useful.

- The `requirements.txt` file should be used to keep track of required dependencies for the project and should ideally include specific package versions for future reproducability.

- The `saved` folder is versioned using DVC and includes subfolders for `figures` and `models`.

- The `scripts` folder contains python script files for evaluation (`eval.py`), data processing (`process.py`), and training (`train.py`).

- The `src` package should contain source code files and testing.
    - The `model` subfolder should include source code related to model architecture and usage.
    - The `test` subfolder should include unit tests to verify code integrity.
    - The `utils` subfolder should include utility functions used by notebooks and script files.

## Getting Started

1. Installing Dependencies

```
python3 -m venv .env
source .env/bin/activate
pip install -r requirements.txt
```

2. Initialize Data Version Control

If dvc is already initialized, skip to step 4.

```
dvc init
dvc config core.autostage true
git commit -m "Initialize DVC"

git rm -r --cached 'config'
dvc add config
git commit -m "Add config folder to DVC"

git rm -r --cached 'data'
dvc add data
git commit -m "Add data folder to DVC"

git rm -r --cached 'saved'
dvc add saved
git commit -m "Add saved folder to DVC"

git push
```

3. Create DVC Remote

Follow tutorial [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) to create S3 bucket

```
dvc remote add -d remote s3://<insert bucket name here>/dvc
```

```
dvc remote modify remote region <insert bucket region here>
```

```
git add .dvc/config
git commit -m "Added S3 Remote"
git push
```

4. Add AWS Credentials to DVC Remote 

```
dvc remote modify --local remote access_key_id <insert AWS_ACCESS_KEY_ID here>
```

```
dvc remote modify --local remote secret_access_key <insert AWS_SECRET_ACCESS_KEY here>
```

## Push to Assembla

If you are using Assembla for code versioning,

```
git remote remove origin
git remote add origin git@git.assembla.com:<insert .git link here>
git push --set-upstream origin main
```

## Using DVC

### Adding Files

To add new files to DVC or version existing data changes,

```
dvc add <name of file/folder>
```

If you are adding new data,

```
git commit -m “Added <name of file/folder> to dvc”
```

If you are updating existing data,

```
git commit -m “Updated <name of file/folder> with <data changes>”
```

```
git tag -a “<version>” -m “<name of file/folder> version <version>”
git push
dvc push
```

### Checkout Data

To checkout a specific version of a file or folder,

```
git checkout tags/<version> <name of file/folder>
dvc pull
```

To go back to the current data version,

```
git checkout <current branch>
dvc pull
```

## Jupyter Notebook

To use jupyter notebooks within your venv environment,

```
pip install jupyter ipykernel
python -m ipykernel install --user --name=.env
```
