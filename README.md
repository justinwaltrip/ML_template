# Machine Learning Template

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
echo "!/**/.gitkeep" >> .dvcignore
dvc add data
git add data.dvc
git commit -m "Add data folder to DVC"
```

```
dvc add saved
git add saved.dvc
git commit -m "Add saved folder to DVC"
```

```
git push
```

### Push to S3

Follow tutorial [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) to create S3 bucket

```
dvc remote add -d remote s3://<insert bucket name here>/<insert folder name here>
```

```
dvc remote modify remote access_key_id <insert AWS_ACCESS_KEY_ID here>
```

```
dvc remote modify remote secret_access_key <insert AWS_SECRET_ACCESS_KEY here>
```

```
dvc push
```
