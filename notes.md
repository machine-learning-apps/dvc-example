1. Install via [installation guide](https://dvc.org/doc/install)

2. [Opt out](https://dvc.org/doc/user-guide/analytics#opting-out) of aggregate usage analytics:

    > dvc config core.analytics false --system



3. Add the data to dvc

    _optional_: get data
    > dvc get https://github.com/iterative/dataset-registry get-started/data.xml -o data/data.xml
      
      In this repo, this will be fetched from s3, because of the contents of `.dvc/config`

    > dvc add data/data.xml

4. Check in metadata to git

    ```bash
    git add data/.gitignore data/data.xml.dvc
    git commit -m "Add raw data"; git push
    ```

5. Add storage

    > dvc remote add -d storage s3://hamel/dvc

6. Commit metadata

    > git commit .dvc/config -m "Configure remote storage"

7. Store data

    > dvc push

8. Change Data

    ```bash
    dvc add data/data.xml
    git commit data/data.xml.dvc -m "Dataset updates"
    dvc push
    ```

9. Download Data
    
    ```bash
    dvc get https://github.com/iterative dataset-registry use-cases/cats-dogs
    ```

## Data Pipelines

You can run data pipelines in DVC which is focused on [reproducability](https://dvc.org/doc/start/data-pipelines#data-pipelines).

