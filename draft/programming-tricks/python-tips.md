# Tips about Python

## Thread and Pool
* concurrent.futures.ThreadPoolExecutor
  * Threads the process and limits them into a Pool of Threads
* concurrent.futures.ProcessPoolExecutor
  * Same with previous but use Process instead

## Async/Await
* asyncio
  * write **concurrent** code using the **async/await** syntax
  * [https://stackabuse.com/python-async-await-tutorial/](https://stackabuse.com/python-async-await-tutorial/)
* [uvloop](https://github.com/MagicStack/uvloop)
  * event loop on top of asyncio

## Reference

{% embed url="https://dev.to/rhymes/how-to-make-python-code-concurrent-with-3-lines-of-code-2fpe" %}



