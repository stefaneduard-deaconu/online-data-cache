# Online Data Cache

## Problem statement

Imagine caching data for a multiprocess functionality. For example, for a given 3D terrain multiple processes compute the shortest path using different path planners and store the solutions inside the same MongoDB document. At the same time, the data may be displayed on multiple dashboard instances.
As you can see, the data must be synced between multiple clients as efficiently as possible. 

One of the biggest throttles is that the data must be serialised and deserialised, and the amount of data that must be fetched as the number of calculations increases.

The out of the box solutions is storing an unique hash that changes each time the data changes, and triggering data fetching on all clients when the local hash differs from the online hash. But this doesn't limit the amount of fetched data.

Because of this, we chose to store to a more efficient caching database (e.g. Redis) the changes that must be applied to switch from an older version of the data, to a newer one.


## Tests and experimentation

This project is more of a question whether this systest is more efficient and what are the use cases where it can be applied. 
We will discover which variables (such as number of concurent processes, number of clients, the amount of data) and based on them we will train a simple regression to choose when to turn the process on.

## Results

We hope that this project can be integrated efficiently into working solutions, to enable a fast to apply plugin that improved performance of existing systems or APIs.
