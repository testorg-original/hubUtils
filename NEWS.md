# hubUtils 0.0.0.9007

* New function `validate_hub_config()` allows maintainers to check the validity of hub config files in a single call. Function `view_config_val_errors()` also modified to create combined report for hub config files from output of `validate_hub_config()`.
* Breaking change: All `model-output` data are expected to have `output_type` & `output_type_id` instead of `type` & `type_id` respectively.

# hubUtils 0.0.0.9006

* `hub_connect()` now automatically determines the `output_type_id` column data type from the tasks.json config file coercing to the highest possible data type, "character" being the lowest denominator.
* Introduced function `create_hub_schema()` for determining the schema for data in a hub's model-output directory from a tasks.json config file.
* `hub_connect()` now allows establishing connections to hubs with multiple file type formats.
* `create_output_type_categorical()` function was renamed to `create_output_type_pmf()`.
* When extracting data via a hub connection, the column containing model identification information, inferred from `model-output` data directory partitions, was renamed from "model" to "model_id".

# hubUtils 0.0.0.9005

* Re-implemented `hub_connect()` function to open connection to `model-output` data
implemented through an `arrow` `FileSystemDataset` object. This allows users to create
custom `dplyr` queries to access model output data.

# hubUtils 0.0.0.9004

* Added functionality to help create json configuration files.

# hubUtils 0.0.0.9003

* Added `validate_config()` function to validate json configuration files against Hub 
schema as well as function `view_config_val_errors()` for viewing a concise and easier to 
navigate table of validation errors.
* Added a `NEWS.md` file to track changes to the package.