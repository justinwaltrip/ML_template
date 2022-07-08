# Machine Learning Template

## Repository Structure

```
├── Makefile
├── README.md
├── data
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
└── utils
```

- The `Makefile` should be used to setup the repository (ex. install required OS libraries) or to save complex commands/workflows such as training or running experiments with many command line arguments.

- The `data` folder is versioned using DVC and includes subfolders for `raw` and `processed` data.

- The `notebooks` folder should be used for data exploration or in other situations where data visualization may be useful.

- The `requirements.txt` file should be used to keep track of required dependencies for the project and should ideally include specific package versions for future reproducability.

- The `saved` folder is versioned using DVC and includes subfolders for `figures` and `models`.

- The `scripts` folder contains python script files for evaluation (`eval.py`), data processing (`process.py`), and training `train.py`.

- The `utils` folder should include utility functions used by notebooks and script files.

## Getting Started

### Installing Dependencies

```
python3 -m venv .env
source .env/bin/activate
pip install -r requirements.txt
```

### Initialize Data Version Control

```
dvc init
dvc config core.autostage true
git commit -m "Init DVC"

rm data/**/.gitkeep
git rm -r --cached 'data'
dvc add data
git commit -m "Add data folder to DVC"

rm saved/**/.gitkeep
git rm -r --cached 'saved'
dvc add saved
git commit -m "Add saved folder to DVC"

git push
```

### Push DVC files to S3

Follow tutorial [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) to create S3 bucket

```
dvc remote add -d remote s3://<insert bucket name here>/dvc
```

```
dvc remote modify remote region <insert bucket region here>
```

```
dvc remote modify remote access_key_id <insert AWS_ACCESS_KEY_ID here>
```

```
dvc remote modify --local remote secret_access_key <insert AWS_SECRET_ACCESS_KEY here>
```

```
git add .dvc/config
git commit -m "Added S3 Remote"
git push
dvc push
```

### Jupyter Notebook

To use jupyter notebooks within your venv environment,

```
pip install jupyter ipykernel
python -m ipykernel install --user --name=.env
```
