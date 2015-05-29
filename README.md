## Little demos of Celery usage

### Non example files
* `celeryconfig.py` - default configuration of the Celery daemon I use across all examples
* `tasks.py` - celery tasks I invoke in all examples
* `docker-compose.yml` - used to spin up a container with the redis which is used as a broker and a result storage. There is no `celery` container because the default one does not have `eventlet` module

### Examples
* `01-synchroonous-execution.py` - execute a group of tasks with blocking I/O in one Celery worker 
* `02-synchroonous-execution-multiple-workers.py` - same as the previous example but with multiple workrs
* `03-async-execution-with-eventlet.py` - execute a group of tasks with eventlet option enabled in celery and with non-blocking I/O


### Running examples

To run an example which does not use `eventlet` (like `01-synchroonous-execution`) just type:

	celery worker  --loglevel=info  -A 01-synchroonous-execution

For running eventlet examples (like `03-async-execution-with-eventlet`) use:

	celery worker  --loglevel=info  -A 03-async-execution-with-eventlet -P eventlet

We need to specify the `-P eventlet` in a command line and can't set this setting in code because the docs [say](https://celery.readthedocs.org/en/latest/configuration.html#celeryd-pool):

> Never use this option to select the eventlet or gevent pool. You must use the -P option instead, otherwise the monkey patching will happen too late and things will break in strange and silent ways.