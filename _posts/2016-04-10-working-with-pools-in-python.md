---
layout: post
title:  Working with Pools in python
date:   2016-04-10 01:53:18 +1100
categories: python parallel
---

# Problem - long running single-threaded simulations
I was writting a simulation for the [6.00.2x - Introduction to Computational Thinking 
and Data Science by MITx on EDX](https://www.edx.org/course/introduction-computational-thinking-data-mitx-6-00-2x-3).
One of problem sets required a simulation to be run few hundred times to collect enough samples.
It took 4-5 minutes to get results for few hundred trials. 

The base version of the simulation was written in Python 2.7
and executed in a single thread.

I started to explore how to use Python multiprocessing library to utilise all of my CPUs to get the results faster.

## Base solution
I've started with writting a function that runs a single simulation run.

```python
def runSimulation(numViruses, maxPop, maxBirthProb, clearProb,
                  resistances, mutProb, numStepsBeforeDrug, numStepsAfterDrug):
    
    # Lots of happening in here    
    return (numViruses, numResistantViruses)
```

I call this function in a trivial way:

```python
def simulate(numTrials):
    # Setting up simulation environment - removed for brevity 
    for t in range(numTrials):
        total, resistant = runSimulation(num_viruses,
                                         max_pop,
                                         max_birth_prob,
                                         clear_prob,
                                         resistances,
                                         mut_prob,
                                         num_steps_before_drug,
                                         num_steps_after_drug)
    
    # Plotting results - removed for brevity
```

## Possible solution - using Pool from multiprocessing library
I started exploring [multiprocessing library](https://docs.python.org/2/library/multiprocessing.html)
and its capacity of using process pools.

Sample from Python doco:

```python
from multiprocessing import Pool
import time

def f(x):
    return x*x

if __name__ == '__main__':
    pool = Pool(processes=4)              # start 4 worker processes

    result = pool.apply_async(f, (10,))   # evaluate "f(10)" asynchronously in a single process
    print result.get(timeout=1)           # prints "100" unless your computer is *very* slow

    print pool.map(f, range(10))          # prints "[0, 1, 4,..., 81]"

    it = pool.imap(f, range(10))
    print it.next()                       # prints "0"
    print it.next()                       # prints "1"
    print it.next(timeout=1)              # prints "4" unless your computer is *very* slow

    result = pool.apply_async(time.sleep, (10,))
    print result.get(timeout=1)           # raises multiprocessing.TimeoutError
```

Pool method `map` seemed to be a good choice - it takes an iterable and executes
a function, passes in the first argument, for each of items in the iterable. 

## Mapping arguments
My function accepted 8 arguments and I wanted exactly N runs with the same arguments 
to be performed. Also I wanted my parallel execution pattern to be universal -
few more excercises to go and I had to write separate simulation functions 
for other scenarios.

### Simple wrapper
First things first, we'll need an import:

```python
from multiprocessing import Pool 

```

Next, I've created a wrapper that will help me pass [a packed argument list](https://docs.python.org/2/tutorial/controlflow.html#unpacking-argument-lists)
pass it to a simulation runs in a positional manner: 

```python
def runSimulationWrapper(args):
    return runSimulation(*args)

```

I've created a simple function that will set up the parallel execution:

```python
def runParallel(args, num_trials):
    try:
        p_args = [args for i in range(num_trials)]
        pool = Pool(8)                                                  
        arg_len = len(p_args)
        p_result = pool.map(runSimulationWrapper, p_args)
        return p_result
    finally:
        pool.close()
        pool.join()    

```

I modified my main `simulate` function to use the function above

```python

def simulate(numTrials):
    # Setting up simulation environment - removed for brevity 
    
    # Packing arguments
    args = [num_viruses,
            max_pop,
            max_birth_prob,
            clear_prob,
            resistances,
            mut_prob,
            num_steps_before_drug,
            num_steps_after_drug]

    results = runParallel(args, numTrials)
    
    # Plotting results - removed for brevity
``` 


## Executing simulations

In my sequential approach I just dropped a call to the `simulate` method 
to the bottom of my file and used VSCode or IDLE to run it.

After modifying my execution model to parallel - my code just hanged. 
I spent few hours checking different samples of using `multiprocessing` library
and some of them ran nicely while other hanged, finally I found what was the problem.

As stated in [Programming guildelines - Windows](https://docs.python.org/2.7/library/multiprocessing.html#windows)
we need to make sure that the main module can be safely imported by protecting the “entry point” of the program 

So, instead of:

```python
simulate(100)

```

Do this *

```python
if __name__ == '__main__':
    simulate(100)
    
``` 

\* and read docos before spending hours debugging solutions from the internet  