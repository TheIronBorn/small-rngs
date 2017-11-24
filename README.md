small-rngs
====

A collection of small pseudorandom number generators in Rust.

The intention of this repository is to collect small PRNGs, to make it easier
to comparing them.

This requires rustc nightly to build, because some RNGs need support for `u128`.

Note: not all implementations of RNGs are verified to be correct yet.

## Currently implemented RNGs
Various lesser-known PRNGs:
- `GjRng`: A small random number generator by Geronimo Jones.
- `Jsf32Rng`: A small random number generator designed by Bob Jenkins.
- `Jsf64Rng`: A small random number generator designed by Bob Jenkins
  (64-bit variant).
- `Sfc32Rng`: A small random number generator designed by Chris Doty-Humphrey.
- `Sfc64Rng`: A small random number generator designed by Chris Doty-Humphrey
  (64-bit variant).
- `Sapparot32Rng`: The Sapparoth-2 RNG by Ilya Levin (32-bit variant).
- `Sapparot64Rng`: The Sapparoth-2 RNG by Ilya Levin (64-bit variant).
- `Velox3bRng`: A small random number generator designed by Elias Yarrkov.

Xorshift family:
- `Xorshift128_32Rng`: An Xorshift random number generator (128/32-bit variant).
- `Xorshift128_64Rng`: An Xorshift random number generator (128/64-bit variant).
- `Xorshift128PlusRng`: The Xorshift128+ random number generator.
- `Xoroshiro128PlusRng`: The Xoroshiro128+ random number generator.
- `Xoroshiro64PlusRng`: A 32-bit variant of Xoroshiro128+,
  with just 64 bits of state.
- `XorshiftMultWT32Rng`
- `XorshiftMultWT64Rng`

PCG family:
- `PcgXsh64LcgRng`: A PCG random number generator (XSH 64/32 (LCG) variant).
- `PcgXsl128LcgRng`: A PCG random number generator (XSL 128/64 (LCG) variant).

## Benchmarks

Result of `cargo bench`:
```rust
test gen_u32_gj                  ... bench:       3,333 ns/iter (+/- 3) = 1200 MB/s
test gen_u32_jsf32               ... bench:       2,229 ns/iter (+/- 1) = 1794 MB/s
test gen_u32_jsf64               ... bench:       2,312 ns/iter (+/- 4) = 1730 MB/s
test gen_u32_pcg_xsh_64_lcg      ... bench:       1,222 ns/iter (+/- 13) = 3273 MB/s
test gen_u32_pcg_xsl_64_lcg      ... bench:       1,197 ns/iter (+/- 2) = 3341 MB/s
test gen_u32_pcg_xsl_128_mcg     ... bench:       1,461 ns/iter (+/- 1) = 2737 MB/s
test gen_u32_sapparoth_32        ... bench:       2,544 ns/iter (+/- 4) = 1572 MB/s
test gen_u32_sapparoth_64        ... bench:       2,545 ns/iter (+/- 10) = 1571 MB/s
test gen_u32_sfc_32              ... bench:         980 ns/iter (+/- 4) = 4081 MB/s
test gen_u32_sfc_64              ... bench:       1,221 ns/iter (+/- 1) = 3276 MB/s
test gen_u32_velox               ... bench:       2,007 ns/iter (+/- 35) = 1993 MB/s
test gen_u32_xoroshiro_128_plus  ... bench:       1,196 ns/iter (+/- 1) = 3344 MB/s
test gen_u32_xoroshiro_64_plus   ... bench:       1,097 ns/iter (+/- 1) = 3646 MB/s
test gen_u32_xorshift_128_32     ... bench:       1,082 ns/iter (+/- 2) = 3696 MB/s
test gen_u32_xorshift_128_64     ... bench:         977 ns/iter (+/- 3) = 4094 MB/s
test gen_u32_xorshift_128_plus   ... bench:       1,186 ns/iter (+/- 3) = 3372 MB/s
test gen_u32_xorshift_mult_wt_32 ... bench:       1,127 ns/iter (+/- 18) = 3549 MB/s
test gen_u32_xorshift_mult_wt_64 ... bench:       1,278 ns/iter (+/- 2) = 3129 MB/s
test gen_u32_xsm32               ... bench:       2,511 ns/iter (+/- 8) = 1592 MB/s
test gen_u32_xsm64               ... bench:       2,423 ns/iter (+/- 8) = 1650 MB/s
test gen_u64_gj                  ... bench:       3,333 ns/iter (+/- 3) = 2400 MB/s
test gen_u64_jsf32               ... bench:       3,078 ns/iter (+/- 3) = 2599 MB/s
test gen_u64_jsf64               ... bench:       2,311 ns/iter (+/- 5) = 3461 MB/s
test gen_u64_pcg_xsh_64_lcg      ... bench:       3,603 ns/iter (+/- 6) = 2220 MB/s
test gen_u64_pcg_xsl_64_lcg      ... bench:       3,439 ns/iter (+/- 19) = 2326 MB/s
test gen_u64_pcg_xsl_128_mcg     ... bench:       1,468 ns/iter (+/- 6) = 5449 MB/s
test gen_u64_sapparoth_32        ... bench:       4,008 ns/iter (+/- 13) = 1996 MB/s
test gen_u64_sapparoth_64        ... bench:       2,546 ns/iter (+/- 5) = 3142 MB/s
test gen_u64_sfc_32              ... bench:       3,218 ns/iter (+/- 9) = 2486 MB/s
test gen_u64_sfc_64              ... bench:         980 ns/iter (+/- 3) = 8163 MB/s
test gen_u64_velox               ... bench:       3,667 ns/iter (+/- 35) = 2181 MB/s
test gen_u64_xoroshiro_128_plus  ... bench:       1,101 ns/iter (+/- 3) = 7266 MB/s
test gen_u64_xoroshiro_64_plus   ... bench:       3,624 ns/iter (+/- 25) = 2207 MB/s
test gen_u64_xorshift_128_32     ... bench:       2,638 ns/iter (+/- 23) = 3032 MB/s
test gen_u64_xorshift_128_64     ... bench:         979 ns/iter (+/- 3) = 8171 MB/s
test gen_u64_xorshift_128_plus   ... bench:       1,186 ns/iter (+/- 3) = 6745 MB/s
test gen_u64_xorshift_mult_wt_32 ... bench:       3,416 ns/iter (+/- 12) = 2341 MB/s
test gen_u64_xorshift_mult_wt_64 ... bench:       1,313 ns/iter (+/- 3) = 6092 MB/s
test gen_u64_xsm32               ... bench:       3,901 ns/iter (+/- 17) = 2050 MB/s
test gen_u64_xsm64               ... bench:       2,423 ns/iter (+/- 8) = 3301 MB/s
```

Result of `cargo bench --target i686-unknown-linux-musl`:
```rust
test gen_u32_gj                  ... bench:       8,787 ns/iter (+/- 118) = 455 MB/s
test gen_u32_jsf32               ... bench:       2,680 ns/iter (+/- 34) = 1492 MB/s
test gen_u32_jsf64               ... bench:       7,595 ns/iter (+/- 104) = 526 MB/s
test gen_u32_pcg_xsh_64_lcg      ... bench:       2,953 ns/iter (+/- 75) = 1354 MB/s
test gen_u32_pcg_xsl_64_lcg      ... bench:       2,948 ns/iter (+/- 29) = 1356 MB/s
test gen_u32_pcg_xsl_128_mcg     ... bench:      12,736 ns/iter (+/- 121) = 314 MB/s
test gen_u32_sapparoth_32        ... bench:       2,615 ns/iter (+/- 27) = 1529 MB/s
test gen_u32_sapparoth_64        ... bench:       8,442 ns/iter (+/- 40) = 473 MB/s
test gen_u32_sfc_32              ... bench:       2,434 ns/iter (+/- 7) = 1643 MB/s
test gen_u32_sfc_64              ... bench:       4,125 ns/iter (+/- 14) = 969 MB/s
test gen_u32_velox               ... bench:       2,934 ns/iter (+/- 7) = 1363 MB/s
test gen_u32_xoroshiro_128_plus  ... bench:       2,442 ns/iter (+/- 21) = 1638 MB/s
test gen_u32_xoroshiro_64_plus   ... bench:       1,223 ns/iter (+/- 14) = 3270 MB/s
test gen_u32_xorshift_128_32     ... bench:       1,475 ns/iter (+/- 60) = 2711 MB/s
test gen_u32_xorshift_128_64     ... bench:       2,567 ns/iter (+/- 59) = 1558 MB/s
test gen_u32_xorshift_128_plus   ... bench:       2,444 ns/iter (+/- 17) = 1636 MB/s
test gen_u32_xorshift_mult_wt_32 ... bench:       1,715 ns/iter (+/- 29) = 2332 MB/s
test gen_u32_xorshift_mult_wt_64 ... bench:       3,497 ns/iter (+/- 51) = 1143 MB/s
test gen_u32_xsm32               ... bench:       3,189 ns/iter (+/- 157) = 1254 MB/s
test gen_u32_xsm64               ... bench:       6,007 ns/iter (+/- 283) = 665 MB/s
test gen_u64_gj                  ... bench:       8,812 ns/iter (+/- 125) = 907 MB/s
test gen_u64_jsf32               ... bench:       3,838 ns/iter (+/- 63) = 2084 MB/s
test gen_u64_jsf64               ... bench:       7,661 ns/iter (+/- 73) = 1044 MB/s
test gen_u64_pcg_xsh_64_lcg      ... bench:       6,335 ns/iter (+/- 111) = 1262 MB/s
test gen_u64_pcg_xsl_64_lcg      ... bench:       5,769 ns/iter (+/- 68) = 1386 MB/s
test gen_u64_pcg_xsl_128_mcg     ... bench:      13,802 ns/iter (+/- 254) = 579 MB/s
test gen_u64_sapparoth_32        ... bench:       4,360 ns/iter (+/- 82) = 1834 MB/s
test gen_u64_sapparoth_64        ... bench:       8,491 ns/iter (+/- 207) = 942 MB/s
test gen_u64_sfc_32              ... bench:       3,568 ns/iter (+/- 15) = 2242 MB/s
test gen_u64_sfc_64              ... bench:       4,914 ns/iter (+/- 17) = 1628 MB/s
test gen_u64_velox               ... bench:       5,282 ns/iter (+/- 82) = 1514 MB/s
test gen_u64_xoroshiro_128_plus  ... bench:       2,933 ns/iter (+/- 11) = 2727 MB/s
test gen_u64_xoroshiro_64_plus   ... bench:       3,850 ns/iter (+/- 65) = 2077 MB/s
test gen_u64_xorshift_128_32     ... bench:       4,591 ns/iter (+/- 59) = 1742 MB/s
test gen_u64_xorshift_128_64     ... bench:       2,638 ns/iter (+/- 91) = 3032 MB/s
test gen_u64_xorshift_128_plus   ... bench:       3,014 ns/iter (+/- 5) = 2654 MB/s
test gen_u64_xorshift_mult_wt_32 ... bench:       3,982 ns/iter (+/- 52) = 2009 MB/s
test gen_u64_xorshift_mult_wt_64 ... bench:      11,666 ns/iter (+/- 111) = 685 MB/s
test gen_u64_xsm32               ... bench:       4,346 ns/iter (+/- 190) = 1840 MB/s
test gen_u64_xsm64               ... bench:       6,282 ns/iter (+/- 311) = 1273 MB/s
```
