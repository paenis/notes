rate as a function of index size (# k-mers), normalized/showing scaling for # workers?

- ~~pick a set of 10k accessions that we already have and download the corresponding unitigs (.fa.zst)~~
	- ~~modify the index to accept/process 31-mers~~
- ~~do a comparison with these against the same set of squeakrs, if nothing weird happens then switch to unitigs for everything~~
- kmer abundance filtering in order to compare against Logan
	- if Logan has a JSON API, make out API format compatible to make comparison easier
- follow up with prashant about measuring insert throughput
	- scaling in reverse..
- variance of index size across machines


- take query latency for fixed transcript length (1-2k) every (approx) X samples (scaling experiment)
	- separately, query latency scaling vs transcript length at largest index size
- variance between size of each worker at various index sizes
- continuous index size w/o buffer cqf mem, log y scale
- kmer throughput slop thing

s3 interface for workers !?
