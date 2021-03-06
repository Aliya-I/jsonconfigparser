## Description

Utility that allows to read and parse json config files.

Possible to specify links to the default values in the config (See Usage section).

## Installation

1. Install python 3.6
2. Ensure pip, setuptools, and wheel are installed and up to date
   
`python -m pip install --upgrade pip setuptools wheel`
 
3. Create virtual enviroment (make sure that is not part of the project)

`python -m venv <ENV NAME>`

or 

`python -m venv c:\path\to\<ENV NAME>`

4. Active virtual enviroment

`c:\path\to\<ENV NAME>\Script\activate`

5. Install all project dependencies if needed

`pip install -r requirements.txt`

NOTE: if pypandoc didn't get installed. [Please install it manually](https://pypi.python.org/pypi/pypandoc)


## Usage

Example of the config file:

```
C:\User\test\qa_hotfix_config.json

{
    "defaults": {
        "dataBaseUrl": "http://db:5000"
    },
    "dataBase1": "<defaults.dataBaseUrl>",
    "dataBase2": "<defaults.dataBaseUrl>"
}
```

1. Specify that lib in your project dependencies
2. inport `from jsonconfigparser.json_config_parser import JsonConfigParser`
3. create instance of the class passing config folder path and options

```
config_path = 'C:\User\test'
json_config_parser = JsonConfigParser(config_path,
                        options={'env': {'env': 'qa', 'branch': 'hotfix'},
                                 'file_pattern': '{env[name]}_{env[branch]}_config'})
config = json_config_parser.get()
file_path = json_config_parser.get_config_file_path()
print(config['dataBase1'])
print(file_path)

>> http://db:5000
>> C:\User\test\qa_hotfix_config.json
```

NOTE: `options` is optional argumet. It is possible to speficy `config_path` as `C:\User\test\qa_hotfix_config.json`


## Uploading project to PyPi

1. change version in `setup.py`
2. upload changes to PyPi server

`python setup.py sdist upload -r <Repository URL to the PyPi server>`


## Run unit tests

1. From Visual Studio
   1. Click `Test` -> `Run` -> `All Test`
   2. View Test run in `Test Explorer`
2. From CLI
   1. Navigate into project directory 
   2. `python -m unittest`

