# logging

* logging的普通模式： Basicconfig
* 使用handler，logger

```
logging.info --> logger --> handler
                            ^
                            |
                            |
                        formatter
```

##### 日记记录的机制：

1. logger是有继承的，a继承默认的root，a.b继承a
2. logger有propagate，如果该字段为True，那么日志除了本层处理外，还会传给上一级的handler
3. logger有日志级别，如果日志的级别小于这个级别，那么日志不会记录，本层流程结束
4. handler有日志级别。同logger的日志级别逻辑
5. 一个logger可以有多个handler
6. logging.info这种会默认使用root的logger
7. logger.info则使用对应的logger的日志打印

logger的日志级别时入口过滤，handler是出口过滤

以下是root的logger的一个example，使用

```python
xlog = Log.XlsLog()
xlog.init_log(logtype=['stdout', os.getenv('I_WANT_EXCEL', 'sky_gitlab_robot')])
```

定义logger，handler，formatter

```python
import logging
import os
import pathlib
from abc import ABC, abstractmethod
from logging.handlers import RotatingFileHandler


class SelfHandler(RotatingFileHandler):
    pass


class BindLog(ABC):
    def __init__(self, logger, loglevel):
        self.logger = logger
        self.loglevel = loglevel
        self.formatter = None
        self.handler = None

    @abstractmethod
    def _formatter(self):
        pass

    @abstractmethod
    def _handler(self):
        pass

    def bind(self):
        self._formatter()
        self._handler()

        self.handler.setFormatter(self.formatter)
        self.handler.setLevel(self.loglevel)
        self.logger.addHandler(self.handler)


class BindStreamLog(BindLog):
    def _formatter(self):
        self.formatter = logging.Formatter(
            '%(asctime)s <%(levelname)s> %(message)s')

    def _handler(self):
        self.handler = logging.StreamHandler()


class BindFileLog(BindLog):
    def _formatter(self):
        self.formatter = logging.Formatter(
            '%(asctime)s [%(name)s]: <%(levelname)s> %(message)s '
            '[%(filename)s:%(lineno)d:%(funcName)s]')

    def _handler(self):
        file_name = pathlib.Path(__file__).parent.parent.absolute().as_posix() + '/log'
        os.makedirs(file_name, int('0755', 8), exist_ok=True)
        self.handler = SelfHandler(f'{file_name}/issue.log',
                                   maxBytes=10 * 1024 * 1024)


class XlsLog:
    def init_log(self, logtype='stdout', loglevel=logging.INFO):
        logger = logging.getLogger()

        if logger.hasHandlers():
            return

        if not logtype:
            return

        if isinstance(logtype, str):
            logtype = [logtype]

        logger.setLevel(logging.DEBUG)
        for t in logtype:
            if t == 'stdout':
                BindStreamLog(logger, loglevel).bind()
            else:
                BindFileLog(logger, loglevel).bind()
                logger.name = t
```
