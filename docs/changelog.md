# Changelog

All notable changes to this project will be documented in this file.

This project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

No changes yet.

## [v0.11.0](https://github.com/NGWPC/ripple1d/releases/tag/v0.11.0)

### API

This version renames an endpoint.
**This is a breaking change; there is no backwards-compatible alias.**

#### create_scenarios_db (renamed from create_rating_curves_db)

- `create_rating_curves_db` is now `create_scenarios_db`.
- The records it writes are computed model scenarios (a discharge, and for `kwse` plans a downstream stage, with the resulting water surface elevations), not rating curves.
- The output table is renamed from `rating_curves` to `scenarios` to match, and the result key returned by the endpoint is renamed from `rating_curve_database` to `scenario_database`.

## [v0.10.4](https://github.com/NGWPC/ripple1d/releases/tag/v0.10.4)

### API

This version contains new optional args for `create_fim_lib` and `conflate_model`:

#### create_fim_lib

- `cog` (boolean): This is a boolean indicating if the depth grids should be cloud optimized geotiffs or not.

#### conflate_model

- `min_flow_multiplier` (float): This is the number that will be multiplied by the NWM "high flow threshold" to define the low_flow value in the conflation json.
- `max_flow_multiplier` (float): This is the number that will be multiplied by the NWM 100-year flow to define the high_flow value in the conflation json.

#### extract_submodel

- `min_flow_multiplier_ras` (float): This is the number that will be multiplied by the RAS min modeled flow.
  Default is 1.
- `max_flow_multiplier_ras` (float): This is the number that will be multiplied by the RAS max modeled flow.
  Default is 1.
- `ignore_ras_flows` (bool): Whether to ignore HEC-RAS min and max flow when defining flow ranges.
  Default is False.
- `ignore_nwm_flows` (bool): Whether to ignore NWM min and max flow when defining flow ranges.
  Default is False.

## [v0.10.1-v0.10.3](https://github.com/NGWPC/ripple1d/releases/tag/v0.10.3)

### API

This version contains new args for the `conflate_model` and `compute_conflation_metrics` endpoints:

#### extract_submodel

- `model_name` (str): This is the name of the source model.
  Example: Red River.prj -> Red River (model_name)

#### create_ras_terrain

- `terrain_agreement_ignore_error` (bool): If true, this will log and ignore any errors encountered in the terrain agreement calculation process.

## [v0.10.0](https://github.com/NGWPC/ripple1d/releases/tag/v0.10.0)

### API

This version contains new args for the `conflate_model` and `compute_conflation_metrics` endpoints:

#### conflate_model

- `model_name` (str): This is the name of the source model.
  Example: Red River.prj -> Red River (model_name)

#### compute_conflation_metrics

- `model_name` (str): This is the name of the source model.
  Example: Red River.prj -> Red River (model_name)

## [v0.8.0-v0.8.3](https://github.com/NGWPC/ripple1d/releases/tag/v0.8.3)

### API

This beta version contains new args for the `create_ras_terrain` endpoint:

#### create_ras_terrain

- `terrain_agreement_resolution` (float): This is the maximum distance allowed between the vertices used to calculate terrain agreement metrics.
  It is in the units of the HEC-RAS model.

#### jobs

- `f` (json or html): Default value is json.
  Determines the response format of the endpoint.

## [v0.7.0](https://github.com/NGWPC/ripple1d/releases/tag/v0.7.0)

### API

This beta version contains:

#### New endpoints

- `create_rating_curves_db`: creates rating curve using results from `run_known_wse` and `run_incremental_normal_depth` results.
- `jobs`: added endpoints to view job `results`, `metadata`, and `logs`.

#### New args

- `write_depth_grids` (bool) added to `run_known_wse` and `run_incremental_normal_depth` endpoints.

## [v0.6.0-v0.6.3](https://github.com/NGWPC/ripple1d/releases/tag/v0.6.3)

### API

This beta version contains new args for the `create_fim_lib` endpoint:

#### create_fim_lib

- `library_directory`: Specifies the output directory for the FIM grids and database.
- `cleanup`: Boolean indicating if the ras HEC-RAS output grids should be deleted or not.

## [v0.5.0](https://github.com/NGWPC/ripple1d/releases/tag/v0.5.0)

### API

This beta version contains new endpoints:

- `geom_to_gpkg`: Extract the data from a model source dirctory to a gepoackage.
- `conflate`: Conflate all reaches from the NWM network corresponding to the source model.
- `conflation_metrics`: Apply conflation metrics for a conflated source model.

## [v0.4.1-v0.4.2](https://github.com/NGWPC/ripple1d/releases/tag/v0.4.2)

This beta version contains the endpoints included in the first production testing release.

### Configuration

Note that the following variables should be set in the postman environment.

```yaml
postman variables:

- key: url
  value: localhost
  type: string
  description: The url of the ripple1d API

- key: source_model_directory
  value: "~\\repos\\ripple1d\\tests\\ras-data\\Baxter"
  type: string
  description: The source model directory (this needs to point to local directory where the source HEC-RAS model is stored)

- key: submodels_base_directory
  value: "~\\repos\\ripple1d\\tests\\ras-data\\Baxter\\submodels"
  type: string
  description: The base directory for the submodels (this needs to point to local directory where submodels generated by ripple1d are stored)

- key: nwm_reach_id
  value: '2823932'
  type: string
  description: The NWM reach id for the model (the default value included is for the Baxter model)

- key: jobID
  value: ''
  type: string
  description: The job id for the model run (this value is generated by the API)
```

## [v0.3.11](https://github.com/NGWPC/ripple1d/releases/tag/v0.3.11)

This version contains the first experimental endpoints included in the ripple1d API.
