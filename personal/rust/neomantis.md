- https://lib.rs/embedded / https://lib.rs/hardware-support
- https://lib.rs/data-structures
- https://lib.rs/encoding
- https://lib.rs/rust-patterns, lol
- https://rust-lang.github.io/api-guidelines/checklist.html!!!

cqf probably needs the most work; a lot of parts also use raw pointers more than I'd like

for cqf, maybe [[bitvec]] is useful. I think the filter and/or color table uses something like a sparse matrix, need to look at paper

de/serialization of some types (e.g. [[#^a8179c|TableRow]]) currently uses (likely safe, but this is not documented) [`std::slice::from_raw_parts`](https://doc.rust-lang.org/std/slice/fn.from_raw_parts.html) instead of proper transmute to `&[u8]`. something like [[zerocopy]] provides a bounds-checked way to do this. alternatively, use something like [[bincode]] for potential space saving, but disk space/OTW format is not really the issue here

likely a ton of things can benefit from better abstraction, documentation, modularity. an easy first step is making `MergeIndex` and other `type`defs into newtype structs

rewriting large parts of the current implementation is definitely possible once everyone is comfortable enough with rust

most deployment is now handled through the `just` command runner! try to keep it updated

random other ideas:
- replace calls to `libc::mmap` etc. with [[memmap2]]?
- need to add docs to as many things as possible
- unit tests
- benchmarks for any library (cqf) if feasible (via [[criterion]])
- real errors and error handling via [[thiserror]]/[[anyhow]]-like crates
- clap -> [[bpaf]] (low prio)

reading:
- [Rustonomicon](https://doc.rust-lang.org/nightly/nomicon/)
- [Perf book](https://nnethercote.github.io/perf-book/)

### Snippets
```rust
impl TableRow {
	/* ... */
	
	pub fn as_bytes(&self) -> &[u8] {
		// SAFETY: self points to a valid TableRow
		unsafe {
			std::slice::from_raw_parts(
				self as *const TableRow as *const u8,
				std::mem::size_of::<TableRow>(),
			)
		}
	}
}
```

^a8179c
