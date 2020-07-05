# Python CLI - Click

Personally more prefer Click than `argparse`.

Install Click with:

```bash
pip install click
```

or with python2 and python3 compatible:

```bash
pip3 install click
```

For more details, please refer [here](https://click.palletsprojects.com/en/7.x/)

This page serves for simplified cheatsheet for quick reference.

## Basic Examples

### Basic

Click uses decorator on functions to achieve CLI function.

```python
import click

@click.command()
def hello():
    click.echo('Hello World!')

if __name__ == '__main__':
    hello()
```

```bash
$ python hello.py
Hello World!
```

### Arguments and Options

```python
import click

@click.command()
@click.option('--count', default=1, help='number of greetings')
@click.option('--dummy-args', default=1, help='example of multi-options')
@click.argument('name')
def hello(count, name, dummy_args):
    for x in range(count):
        click.echo('Hello %s!' % name)

if __name__ == '__main__':
    hello()
```

```bash
$ python hello.py --help
Usage: hello.py [OPTIONS] NAME

Options:
  --count INTEGER  number of greetings
  --dummy-args  INTEGER  example of multi-options
  --help           Show this message and exit.
```

## Detailed description

### Arguments

Arguments are mandatory inputs, usually takes as 1 param or a list of params with same meaning.

```python
@click.argument(param_decls=None, type=None, required=False, default=None, callback=None, nargs=None, metavar=None, expose_value=True, is_eager=False, envvar=None, autocompletion=None)
```

| Field | Description |
| :--- | :---: |
| param\_decls | [Parameter declarations](python-cli-click.md#parameter-declarations) |
| type | the type that should be used.   Either a [Parameter Type](python-cli-click.md#parameter-types) or a Python type.   The later is converted into the former automatically if supported. |
| required | controls if this is optional or not. |
| default | the default value if omitted. This can also be a callable, in which case it’s invoked when the default is needed without any arguments. |
| callback | a callback that should be executed after the parameter was matched. This is called as fn\(ctx, param, value\) and needs to return the value. Before Click 2.0, the signature was \(ctx, value\). |
| nargs | the number of arguments to match. If not 1 the return value is a tuple instead of single value. The default for nargs is 1 \(except if the type is a tuple, then it’s the arity of the tuple\). |
| metavar | how the value is represented in the help page. |
| expose\_value | if this is True then the value is passed onwards to the command callback and stored on the context, otherwise it’s skipped. |
| is\_eager | eager values are processed before non eager ones. This should not be set for arguments or it will inverse the order of processing. |
| envvar | a string or list of strings that are environment variables that should be checked. |

### Options

Options are inputs that with name declared. Usually they are optional, with default value instead if not assigned in command.

Fields in Arguments is also supported.

```python
@click.option(param_decls=None, show_default=False, prompt=False, confirmation_prompt=False, hide_input=False, is_flag=None, flag_value=None, multiple=False, count=False, allow_from_autoenv=True, type=None, help=None, hidden=False, show_choices=True, show_envvar=False, **attrs)
```

| Field | Description |
| :--- | :---: |
| param\_decls | [Parameter declarations](python-cli-click.md#parameter-declarations) |
| show\_default | controls if the default value should be shown on the help page. |
| show\_envvar | controls if an environment variable should be shown on the help page. |
| prompt | if set to True or a non empty string then the user will be prompted for input. If set to True the prompt will be the option name capitalized. |
| confirmation\_prompt | if set then the value will need to be confirmed if it was prompted for. |
| hide\_input | if this is True then the input on the prompt will be hidden from the user. This is useful for password input. |
| is\_flag | forces this option to act as a flag. The default is auto detection. |
| flag\_value | which value should be used for this flag if it’s enabled. This is set to a boolean automatically if the option string contains a slash to mark two options. |
| multiple | if this is set to True then the argument is accepted multiple times and recorded. This is similar to nargs in how it works but supports arbitrary number of arguments. |
| count | this flag makes an option increment an integer. |
| allow\_from\_autoenv | if this is enabled then the value of this parameter will be pulled from an environment variable in case a prefix is defined on the context. |
| help | the help string. |
| hidden | hide this option from help outputs. |

## Terms Detailed Description

### Parameter Declarations

Examples:

* For an option with \('-f', '--foo-bar'\), the parameter name is foo\_bar.
* For an option with \('-x',\), the parameter is x.
* For an option with \('-f', '--filename', 'dest'\), the parameter name is dest.
* For an option with \('--CamelCaseOption',\), the parameter is camelcaseoption.
* For an arguments with \(\`foogle\`\), the parameter name is foogle. 

### Parameter Types

| Type | Description |
| :--- | :---: |
| click.STRING | Unicode strings |
| click.INT | Integers |
| click.FLOAT | Floating point values |
| click.BOOL | Boolean values   1, yes, y, t, true =&gt; True   0, no, n, f, false =&gt; False |
| click.UUID | UUID values |
| [click.File](https://click.palletsprojects.com/en/7.x/api/#click.File)\(mode='r', encoding=None, errors='strict', lazy=None, atomic=False\) | Auto-load path input and return as file object. Auto-close when the context tear down. |
| click.Path\(exists=False, file\_okay=True, dir\_okay=True, writable=False, readable=True, resolve\_path=False, allow\_dash=False, path\_type=None\) | Path which may not be exist   **resolve\_path** - The path will be parssed as absolute path, except tilde\(~\) |
| click.Choice\(choices, case\_sensitive=True\) | Value only can be within list of _choices_ |
| click.IntRange\(min=None, max=None, clamp=False\) | Integer Range.   **clamp** - the values will be capped if value input exceeds the range |
| click.FloatRange\(min=None, max=None, clamp=False\) | Floating point Range |
| click.DateTime\(formats=None\) | Load date strings and parse into _datetime_   **formats** – A list or tuple of date format strings, in the order in which they should be tried.   Defaults to `%Y-%m-%d`, `%Y-%m-%dT%H:%M:%S`, `%Y-%m-%d %H:%M:%S`. |

