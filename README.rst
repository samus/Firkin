Firkin 0.1
==========
A .NET embeddable Key/Value store using immutable log journalling and in-memory hashing as its storage back end. Inspired by Basho BitCask paper located at http://downloads.basho.com/papers/bitcask-intro.pdf

Uses
====
- Quickly store and retrieve binary data by unique key


Installation
============
Currently using the driver in the GAC is not supported.  Simply copy the driver assembly somewhere and reference it in your project.  It should be deployed in your application's bin directory.  It is not necessary to reference the test assemblies.

Patches
=======
Patches are welcome and will likely be accepted.  By submitting a patch you assign the copyright to me, Arne F. Claassen.  This is necessary to simplify the number of copyright holders should it become necessary that the copyright need to be reassigned or the code re-licensed.  The code will always be available under an OSI approved license.

Roadmap
=======
- Make ``FirkinHash`` IEnumerable
  - allow both exclusive and non-exclusive iteration (i.e. non-exclusive does not block writes)
- Create ``IDictionary<TKey,TValue>`` wrapper around FirkinHash
- Create ``FirkinIndex`` to create secondary indicies into FirkinHash
- Make stream returned by ``Get()`` lazy for large entries, so projection can be done without reading entire entry into memory

Usage
=====

Usage of base store, ``FirkinHash<TKey>``

::

  // create a new store
  var store = new FirkinHash<string>(storageDirectory);

  // store a value
  store.Put(key, valueStream, valueStreamLength);

  // get a value
  var valueStream = store.Get(key);

  // remove a value
  var removed = store.Delete(key);

  // get store size
  var count = store.Count;

  // merge log files to remove overwritten and deleted entries
  store.Merge(); // does not block reads or writes (mostly)

Some unscientific perf data
===========================
The write/random query test of all users from the StackOverflow dump included in the project has shown the following single threaded numbers:

  41k writes/second
  
  80k queries/second


Contributors
============
- Arne F. Claassen (sdether)


