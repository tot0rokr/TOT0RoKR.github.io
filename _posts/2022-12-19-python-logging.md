---
title: "Python logging summary"
last_modified_at: 2022-12-19T00:00:00-09:00
categories:
- Python
tags:
- python
- library
- module
excerpt: "Python logging module"
---

## Simple Example

### In multiple module

```python
# sample_app.py
import logging
import sample_lib

def main():
    logging.basicConfig(
        filename="sample.log",
        level=logging.DEBUG,
        format="%(asctime)s - %(levelname)s - %(message)s",
        datefmt="%I:%M:%S:%p %m/%d/%Y"
    )
    logging.info('main')
    sample_lib.do_something()
    logging.debug('exit')

if __name__ == '__main__':
    main()
```

```python
# sample_lib.py
import logging

def do_something():
    logging.info('do_something')
```

#### Result

```
# sample.log
03:22:14 PM 12/19/2022-INFO-main
03:22:14 PM 12/19/2022-INFO-do_something
03:22:14 PM 12/19/2022-DEBUG-exit
```


## Advanced Example

### Both stream and file

```python
import logging

# create logger
logger = logging.getLogger('advanced_example')
logger.setLevel(logging.DEBUG)

# create formatter
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# create console handler and set level to info
streamhandler = logging.StreamHandler()
streamhandler.setLevel(logging.INFO)

# add formatter to streamhandler
streamhandler.setFormatter(formatter)

# add streamhandler to logger
logger.addHandler(streamhandler)

# create file handler and set level to debug
filehandler = logging.FileHandler("sample.log")
filehandler.setLevel(logging.DEBUG)

# add formatter to filehandler
filehandler.setFormatter(formatter)

# add filehandler to logger
logger.addHandler(filehandler)

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')
```

#### Result

```
# stdout
2022-12-19 15:53:50,295 - advanced_example - INFO - info message
2022-12-19 15:53:50,295 - advanced_example - WARNING - warn message
2022-12-19 15:53:50,296 - advanced_example - ERROR - error message
2022-12-19 15:53:50,296 - advanced_example - CRITICAL - critical message
```

```
# sample.log
2022-12-19 15:53:50,295 - advanced_example - DEBUG - debug message
2022-12-19 15:53:50,295 - advanced_example - INFO - info message
2022-12-19 15:53:50,295 - advanced_example - WARNING - warn message
2022-12-19 15:53:50,296 - advanced_example - ERROR - error message
2022-12-19 15:53:50,296 - advanced_example - CRITICAL - critical message
```


### Configuration file

```python
import logging
import logging.config

logging.config.fileConfig('logging.conf')

# create logger
logger = logging.getLogger('configuration_example')

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')
```

```
# logging.conf
[loggers]
keys=root,configuration_example

[handlers]
keys=streamhandler,filehandler

[formatters]
keys=formatter

[logger_root]
level=DEBUG
handlers=streamhandler

[logger_configuration_example]
level=DEBUG
handlers=streamhandler,filehandler
qualname=configuration_example
propagate=0

[handler_streamhandler]
class=StreamHandler
level=INFO
formatter=formatter
args=(sys.stdout,)

[handler_filehandler]
class=FileHandler
level=DEBUG
formatter=formatter
args=("sample.log,)

[formatter_formatter]
format=%(asctime)s - %(name)s - %(levelname)s - %(message)s
```

#### Result

```
# stdout
2022-12-19 16:08:43,542 - configuration_example - INFO - info message
2022-12-19 16:08:43,542 - configuration_example - WARNING - warn message
2022-12-19 16:08:43,542 - configuration_example - ERROR - error message
2022-12-19 16:08:43,543 - configuration_example - CRITICAL - critical message
```

```
# sample.log
2022-12-19 16:08:43,542 - configuration_example - DEBUG - debug message
2022-12-19 16:08:43,542 - configuration_example - INFO - info message
2022-12-19 16:08:43,542 - configuration_example - WARNING - warn message
2022-12-19 16:08:43,542 - configuration_example - ERROR - error message
2022-12-19 16:08:43,543 - configuration_example - CRITICAL - critical message
```


### Be Needless

```python
import logging
logging.getLogger('needless_example').addHandler(logging.NullHandler())

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')
```

#### Result

```
# print nothing
```
