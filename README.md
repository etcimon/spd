# spd

Scoped Pools D (spd) is a collection of tools that usually require the D Garbage Collector to run. 
However, they have been modified to run on Scoped Pools from memutils.

Scoped pools run as follows:

```D
Json json;
{
  auto pool = ScopedPool();
  json = deserializeJson(str);
  // use json here
} // the data used in json is released and rendered invalid beyond this point
```

The pools automatically run the destructors in reverse order of creation, just like the D Garbage Collector.

To allocate on the pools, all you need is to use `alloc!T` instead of `new T`.

These pools were specially designed to be compatible with fibers (Tasks) from vibe.d, thus are fiber-local when they are run inside fibers.
