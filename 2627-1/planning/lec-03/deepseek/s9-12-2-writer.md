(no output) aexit__
    |     result = await self._task_group.__aexit__(exc_type, exc_val, exc_tb)
    |              ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    |   File "/data/tqlong/lectures/.venv/lib/python3.13/site-packages/anyio/_backends/_asyncio.py", line 847, in __aexit__
    |     raise BaseExceptionGroup(
    |         "unhandled errors in a TaskGroup", self._exceptions
    |     ) from None
    | ExceptionGroup: unhandled errors in a TaskGroup (1 sub-exception)
    +-+---------------- 1 ----------------
      | Traceback (most recent call last):
      |   File "/data/tqlong/lectures/tools/openrouter-mcp/src/openrouter_mcp/bridge.py", line 348, in _worker_session
      |     yield client
      |   File "/data/tqlong/lectures/tools/openrouter-mcp/src/openrouter_mcp/bridge.py", line 503, in run_agent
      |     payload = response.json() if not response.is_error else None
      |               ~~~~~~~~~~~~~^^
      |   File "/data/tqlong/lectures/.venv/lib/python3.13/site-packages/httpx/_models.py", line 832, in json
      |     return jsonlib.loads(self.content, **kwargs)
      |            ~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^
      |   File "/home/tqlong/.local/share/uv/python/cpython-3.13.15-linux-x86_64-gnu/lib/python3.13/json/__init__.py", line 352, in loads
      |     return _default_decoder.decode(s)
      |            ~~~~~~~~~~~~~~~~~~~~~~~^^^
      |   File "/home/tqlong/.local/share/uv/python/cpython-3.13.15-linux-x86_64-gnu/lib/python3.13/json/decoder.py", line 345, in decode
      |     obj, end = self.raw_decode(s, idx=_w(s, 0).end())
      |                ~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^
      |   File "/home/tqlong/.local/share/uv/python/cpython-3.13.15-linux-x86_64-gnu/lib/python3.13/json/decoder.py", line 363, in raw_decode
      |     raise JSONDecodeError("Expecting value", s, err.value) from None
      | json.decoder.JSONDecodeError: Expecting value: line 7 column 1 (char 33)
      +------------------------------------
