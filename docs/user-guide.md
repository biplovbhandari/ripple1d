# User Guide

This section provides a high level overview for using ripple1d for production, including starting the ripple server and submitting jobs.

## Installation

`ripple1d` is registered with [PyPI](https://pypi.org/project/ripple1d) and can be installed simply using python's pip package installer.
Assuming you have Python already installed and setup:

```powershell
pip install ripple1d
```

Note that it is highly recommended to create a python [virtual environment](https://docs.python.org/3/library/venv.html) to install, test, and run ripple.

## Starting the server

The utilities of ripple1d are accessed via an API, and the backend server must be started before any jobs can be processed.

**Start the Ripple Services**:

```powershell
ripple1d start --thread_count 5
```

**Help for the Ripple Services**:

```powershell
ripple1d -h

ripple1d start -h
```

By default, starting ripple1d will launch 2 terminal windows, one for the Flask API and the other for the Huey consumer.
Server logs are stored in the same directory where ripple1d was started.
For example, if you started ripple1d in the directory `C:\Users\user\Desktop`, a new file `C:\Users\user\Desktop\server-logs.jsonld` should be created

Verify that ripple is running by checking the status here: <http://localhost/ping>

```JSON
{"status" : "healthy"}
```

A healthy status indicates that ripple1d is running and waiting for jobs.

## Index of Endpoints

Jobs can be submitted using Postman collections, python clients, curl, or any other software that can communicate via HTTP REST protocol.
The following endpoints reflect a typical workflow for ripple1d.

- [ras_to_gpkg](endpoints/ras-to-gpkg.md)
- [conflate_model](endpoints/conflate-model.md)
- [compute_conflation_metrics](endpoints/compute-conflation-metrics.md)
- [extract_submodel](endpoints/extract-submodel.md)
- [create_ras_terrain](endpoints/create-ras-terrain.md)
- [create_model_run_normal_depth](endpoints/create-model-run-normal-depth.md)
- [run_incremental_normal_depth](endpoints/run-incremental-normal-depth.md)
- [run_known_wse](endpoints/run-known-wse.md)
- [create_fim_lib](endpoints/create-fim-lib.md)

## Example Endpoint Query

```python
import json
import requests

headers = {"Content-Type": "application/json"}
url = f"http://localhost/processes/gpkg_from_ras/execution"
payload = {
      "source_model_directory": 'path/to/ras_dir',
      "crs": 'EPSG:4326',
      "metadata": {
            "some_field": "relevant_data",
            "some_field2": "other data",
      },
   }
response = requests.post(url, data=json.dumps(payload), headers=headers)
```

## Troubleshooting

For help troubleshooting, please add an issue on github at [https://github.com/NGWPC/ripple1d/issues](https://github.com/NGWPC/ripple1d/issues)
