# Setting up the data science framework (initial setup)

### Creating a virtual environment

```
conda create -n dqm_playground_ds python=3.8
conda activate dqm_playground_ds
conda install pip
```

### Installing kedro

```
pip3 install kedro
kedro info
```

### Creating a new project

```
kedro new --starter=spaceflights
> project_name: DQM Playground DS
> repo_name: dqm-playground-ds
> python_package: dqm_playground_ds
```

### Installing dependencies

```
cd dqm-playground-ds
pip install -r src/requirements.txt
```

### Setting up the data

Copy file from eos to local data files (would be nice to use direct call to API in the future)

```
rm data/01_raw/*
cp /eos/user/x/xcoubez/SWAN_projects/ml4dqm-return/starting_data_analysis/pickles/Run_316187_ALL_clusterposition_PXLayer_* data/01_raw/.
```

Add to the catalog
```
vim conf/base/catalog.yml
```

### Modifying the pipelines

Two pipelines are provided in the starter kit:
- a data procession pipeline
- a data science pipeline

### Adding some pipelines

Two additional pipelines could be useful:
- an optional data extraction pipeline allowing to bypass the command line interface by using directly the APIs from the website
- a data visualization pipeline producing time series, correlation plots...

In order to create the new pipelines
```
kedro pipeline create data_extraction
kedro pipeline create data_visualization
```

__Starting with the data visualization pipeline__

The overall idea would be to create a new task on the website (list of runs/lumisections to develop a strategy + list of runs/lumisections to apply the strategy). The data science pipeline (aka this repository) would then allow to produce the predictions from each strategy and re-upload to the website. However, it would be good to produce few plots within the pipeline to check that the pipeline ran successfully.
