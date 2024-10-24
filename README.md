> This Plugin / Repo is being maintained by a community of developers.
There is no warranty given or bug fixing guarantee; especially not by
Programmfabrik GmbH. Please use the GitHub issue tracking to report bugs
and self organize bug fixing. Feel free to directly contact the committing
developers.

# Counter plugin

This server plugin allows automatically setting the values of numeric counter fields when saving data. Counter field values are calculated based on the unique combination of values entered in a defined set of base fields. Please note that the counter field as well as all base fields are expected to be grouped inside the same nested field.

## Installation

The latest version of this plugin can be found [here](https://github.com/programmfabrik/fylr-plugin-counter/releases/latest/download/Counter.zip).

The ZIP can be downloaded and installed using the plugin manager, or used directly (recommended).

## Configuration

All plugin configuration takes place in base configuration.

* *Object types*:
    * *Object type name*: The name of the object type for which to set up the counter
    * *Parent nested fields*:
        * *Path to parent field*: The path to the nested field that contains the counter field and the base fields.
        * *Counter field name*: The name of the counter field to be filled out by the plugin. This has to be a numeric field. The field will only be updated if it is empty and if all base fields have been filled out by the user.
        * *Base field names*: The names of the base fields to consider when updating the counter field. These can be text fields or fields of the [custom data type DANTE](https://github.com/programmfabrik/fylr-plugin-custom-data-type-dante). The combination of the values of these fields is the content that is being counted.

## Example

### Configuration

* *Object type name*: example
* *Path to parent field*: _nested:example__parent
* *Counter field name*: counter
* *Base field names*: place, year

### Result

The field "counter" contains the respective value as generated by the plugin.

Object 1:

    {
        "_nested:example__parent": [
            { "place": "London", "year": "2020", "counter": 1 },
            { "place": "Berlin", "year": "2020", "counter": 1 },
            { "place": "Berlin", "year": "2020", "counter": 2 }
        ]
    }

Object 2:

    {
        "_nested:example__parent": [
            { "place": "London", "year": "2020", "counter": 2 },
            { "place": "Berlin", "year": "2020", "counter": 3 }
            { "place": "Berlin", "year": "2021", "counter": 1 }
        ]
    }
