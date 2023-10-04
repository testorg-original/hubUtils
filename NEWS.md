# hubUtils 0.0.0.9014

* Added `coerce_to_character()` function for coercing all model output columns to character. This can be much faster than coercing to `coerce_to_hub_schema()`, especially for dates.
* Added the following params to `expand_model_out_val_grid()`:
  - `all_character`: allow for returning all character columns.
  - `as_arrow_table`: allow for returning an arrow data table.
  - `bind_model_tasks`: allow for returning list of model task level grids.
* Bug fix. Handle situation in `expand_model_out_val_grid()` when `required_vals_only = TRUE` yet required task ID columns are not consistent across modeling tasks. The function now pads missing task ID column values with `NA`s.

# hubUtils 0.0.0.9013

* Introduced `coerce_to_hub_schema()` function and applied it to `create_model_out_submit_tmpl()` & `expand_model_out_val_grid()` to ensure column data types in returned tibbles are consistent with the hub's schema (#100).
* Fixed bug where optional `mean`/`median` output types where being included erroneously when `required_vals_only = TRUE`.
* Exported function `get_round_task_id_names()` (#99).
* Memoised function `read_config()` (#101).


# hubUtils 0.0.0.9012

* Fixed bug (#95 & #97) which was causing `connect_hub()` to error when `"csv"` was an accepted hub file format but there were no csv in the model output directory. Now `connect_hub()` checks for the presence of files of each accepted file format and only opens datasets for file formats of which files exists. If there are no files of any accepted file_format in the model output directory, the S3 `hub_connection` object returned consists of an empty list. 
* Fixed bug (#96) which was required `hubUtils` to be loaded for `std_colnames` to be internally available.


# hubUtils 0.0.0.9011

* Changed default behaviour of `create_model_out_submit_tmpl()`. Function now, by default, returns rows of complete cases only and the behaviour is controlled by argument `complete_cases_only`. Argument `remove_empty_cols` was also removed.

# hubUtils 0.0.0.9010

* **Support for Hubs using schema earlier than v2.0.0 deprecated**. Currently a warning is issued when interacting with such Hubs. Support will eventually be retired completely and errors will be produced with Hubs using older config schema.
* Added `create_model_out_submit_tmpl()` for generating round specific model output template tibbles (#82).
* Added lower level utilities:
    * `expand_model_out_val_grid()` for creating an expanded grid of valid task ID and output type ID across round modeling tasks and output types.
    * `get_round_idx()`: for getting an integer index of the element in `config_tasks$rounds` that a character round identifier maps to.
    * `get_round_ids()`: for getting a list or character vector of Hub round IDs.
* Added additional `tasks.json` validation checks via `validate_config()`:
    * Check that all task_id and output_type_id values are unique across `required` and `optional` properties.
    * In rounds where `round_id_from_variable` is `TRUE`, check that the specification of the task_id set as `round_id` is consistent across modelling tasks.
    * Check that `round_id` values are unique across rounds.
* Exported object `std_colnames` which contains standard column names used in hubverse model output data files, for use in other hubverse packages (#88).


# hubUtils 0.0.0.9009

* Added `as_model_out_tbl()` function to standardise model output data by converting to a `model_out_tbl` S3 class object. (#32, #33, #63, #64, #66)
* To support back-compatibility with model output data in older hubs, added functions `model_id_merge()` and `model_id_split()` to create `model_id` column from separate `team_abbr` and `model_abbr` columns and vice versa (#63).


# hubUtils 0.0.0.9008

* Added argument `output_type_id_datatype` to `connect_hub()` to allow overriding default behaviour of automatically detecting the `output_type_id` column data type from the `tasks.json` config file (#70).
* Exposed `create_hub_schema()` argument `partitions` to `connect_hub()` function to accommodate custom hub partitioning.
* Added argument `partition_names` to `connect_model_output()` to accommodate custom hub partitioning.
* Added argument `schema` to `connect_model_output()` to allow for overriding default `arrow` schema auto-detection.
* Moved `jsonvalidate` package to Imports so Hub administrator functionality accessible through standard installation.
* Removed argument `format` from `create_hub_schema()` which now creates the same schema from a `tasks.json` config file, regardless of the data file format (#80).



# hubUtils 0.0.0.9007

* New function `validate_hub_config()` allows maintainers to check the validity of hub config files in a single call. Function `view_config_val_errors()` also modified to create combined report for hub config files from output of `validate_hub_config()`.
* Breaking change: All `model-output` data are expected to have `output_type` & `output_type_id` instead of `type` & `type_id` respectively.

# hubUtils 0.0.0.9006

* `connect_hub()` now automatically determines the `output_type_id` column data type from the tasks.json config file coercing to the highest possible data type, "character" being the lowest denominator.
* Introduced function `create_hub_schema()` for determining the schema for data in a hub's model-output directory from a tasks.json config file.
* `connect_hub()` now allows establishing connections to hubs with multiple file type formats.
* `create_output_type_categorical()` function was renamed to `create_output_type_pmf()`.
* When extracting data via a hub connection, the column containing model identification information, inferred from `model-output` data directory partitions, was renamed from "model" to "model_id".

# hubUtils 0.0.0.9005

* Re-implemented `connect_hub()` function to open connection to `model-output` data
implemented through an `arrow` `FileSystemDataset` object. This allows users to create
custom `dplyr` queries to access model output data.

# hubUtils 0.0.0.9004

* Added functionality to help create json configuration files.

# hubUtils 0.0.0.9003

* Added `validate_config()` function to validate json configuration files against Hub 
schema as well as function `view_config_val_errors()` for viewing a concise and easier to 
navigate table of validation errors.
* Added a `NEWS.md` file to track changes to the package.