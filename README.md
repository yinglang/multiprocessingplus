# multiprocplus
multiprocessing plus, a drop-in and easy-use enhancement for multiprcocessing

# install

```shell
# install method 1: from source code
git clone https://github.com/yinglang/multiprocplus
cd multiprocplus
python setup.py install
# install method 2: from pip (TODO)
```

# Usage

```shell
from multiprocplus import multiprocess_for, MultiprocessRunner

# func passed to new process must be global function or 
# member function of global class, and not lambda function
def func(a, b):
    return a * b

if __name__ == "__main__":
    N = 100
    A, B = list(range(N)), list(range(N))
    # run in single process
    C = [func(a, b) for a, b in zip(A, B)]
    print(sum(C))
    # => run in multiprocess
    # only allow to be called under 'if __name__ == "__main__"' of entry script
    C = multiprocess_for(func, [(a, b) for a, b in zip(A, B)], num_process=3)
    print(sum(C))
```

For more usage examples, see []()


# Notice:

- The definition of function passed to new process must be out of 'if __name__ == "__main__"' (global function or member function of global class), 
  and can not be lambda function;
- Code/Function that you do not want to run in new process must be written/called under 'if __name__ == "__main__"' of entry script, 
  or it will run/called in new process.
- Following last note, multiprocess_run must be called in a function called under 'if __name__ == "__main__"' of entry script. 
  Otherwise, new processes will be generated recursively

For error usage examples, to see [test/error_usage](test/error_usage)