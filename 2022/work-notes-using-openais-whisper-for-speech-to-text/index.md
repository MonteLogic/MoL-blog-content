---
title: "Work Notes: Using OpenAI's Whisper for Speech to Text"
date: "2022-12-24"
---

I am tried of being on Mint Linux and having poor speech to text capability so I am going to make a web app and host it on this site.

I am using [this repo](https://github.com/Kabanosk/website_for_whisper) as a starting point.

And I found that repo by looking through the [show and tell page](https://github.com/openai/whisper/discussions/categories/show-and-tell) of OpenAI's [official repo](https://github.com/openai/whisper).

When I set it up viz. install the python scripts and then run the right python file it gives me an error code 500 internal server error.

In detail:

```
NFO:     127.0.0.1:47204 - "GET / HTTP/1.1" 200 OK
INFO:     127.0.0.1:47204 - "GET /main.css HTTP/1.1" 200 OK
/home/monte/.local/lib/python3.8/site-packages/whisper/transcribe.py:78: UserWarning: FP16 is not supported on CPU; using FP32 instead
  warnings.warn("FP16 is not supported on CPU; using FP32 instead")
INFO:     127.0.0.1:57952 - "POST / HTTP/1.1" 500 Internal Server Error
ERROR:    Exception in ASGI application
Traceback (most recent call last):
  File "/home/monte/.local/lib/python3.8/site-packages/uvicorn/protocols/http/h11_impl.py", line 407, in run_asgi
    result = await app(  # type: ignore[func-returns-value]
  File "/home/monte/.local/lib/python3.8/site-packages/uvicorn/middleware/proxy_headers.py", line 78, in __call__
    return await self.app(scope, receive, send)
  File "/home/monte/.local/lib/python3.8/site-packages/fastapi/applications.py", line 270, in __call__
    await super().__call__(scope, receive, send)
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/applications.py", line 124, in __call__
    await self.middleware_stack(scope, receive, send)
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/middleware/errors.py", line 184, in __call__
    raise exc
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/middleware/errors.py", line 162, in __call__
    await self.app(scope, receive, _send)
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/middleware/exceptions.py", line 75, in __call__
    raise exc
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/middleware/exceptions.py", line 64, in __call__
    await self.app(scope, receive, sender)
  File "/home/monte/.local/lib/python3.8/site-packages/fastapi/middleware/asyncexitstack.py", line 21, in __call__
    raise e
  File "/home/monte/.local/lib/python3.8/site-packages/fastapi/middleware/asyncexitstack.py", line 18, in __call__
    await self.app(scope, receive, send)
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/routing.py", line 680, in __call__
    await route.handle(scope, receive, send)
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/routing.py", line 275, in handle
    await self.app(scope, receive, send)
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/routing.py", line 65, in app
    response = await func(request)
  File "/home/monte/.local/lib/python3.8/site-packages/fastapi/routing.py", line 231, in app
    raw_response = await run_endpoint_function(
  File "/home/monte/.local/lib/python3.8/site-packages/fastapi/routing.py", line 162, in run_endpoint_function
    return await run_in_threadpool(dependant.call, **values)
  File "/home/monte/.local/lib/python3.8/site-packages/starlette/concurrency.py", line 41, in run_in_threadpool
    return await anyio.to_thread.run_sync(func, *args)
  File "/home/monte/.local/lib/python3.8/site-packages/anyio/to_thread.py", line 31, in run_sync
    return await get_asynclib().run_sync_in_worker_thread(
  File "/home/monte/.local/lib/python3.8/site-packages/anyio/_backends/_asyncio.py", line 937, in run_sync_in_worker_thread
    return await future
  File "/home/monte/.local/lib/python3.8/site-packages/anyio/_backends/_asyncio.py", line 867, in run
    result = context.run(func, *args)
  File "/home/monte/Scratch/website_for_whisper/src/main.py", line 30, in add_audio
    result = model.transcribe("audio.mp3")
  File "/home/monte/.local/lib/python3.8/site-packages/whisper/transcribe.py", line 84, in transcribe
    mel = log_mel_spectrogram(audio)
  File "/home/monte/.local/lib/python3.8/site-packages/whisper/audio.py", line 111, in log_mel_spectrogram
    audio = load_audio(audio)
  File "/home/monte/.local/lib/python3.8/site-packages/whisper/audio.py", line 42, in load_audio
    ffmpeg.input(file, threads=0)
  File "/home/monte/.local/lib/python3.8/site-packages/ffmpeg/_run.py", line 313, in run
    process = run_async(
  File "/home/monte/.local/lib/python3.8/site-packages/ffmpeg/_run.py", line 284, in run_async
    return subprocess.Popen(
  File "/usr/lib/python3.8/subprocess.py", line 858, in __init__
    self._execute_child(args, executable, preexec_fn, close_fds,
  File "/usr/lib/python3.8/subprocess.py", line 1704, in _execute_child
    raise child_exception_type(errno_num, err_msg, err_filename)
FileNotFoundError: [Errno 2] No such file or directory: 'ffmpeg'

```
