# Machine Learning Template

```
├── Makefile
├── README.md
├── data
│   ├── processed
│   └── raw
├── notebooks
├── out.txt
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
git commit -m "Init DVC"
```

```
rm data/**/.gitkeep
git rm -r --cached 'data'
dvc add data
git add data.dvc .gitignore
git commit -m "Add data folder to DVC"
```

```
rm saved/**/.gitkeep
git rm -r --cached 'saved'
dvc add saved
git add saved.dvc .gitignore
git commit -m "Add saved folder to DVC"
```

```
git push
```

### Push to S3

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
