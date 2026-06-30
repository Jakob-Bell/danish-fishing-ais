# Working with Big Data on a Laptop

The raw AIS files are huge (100M+ rows per year). These are the rules of thumb the team used
during the hackathon to analyse them on normal laptops without freezing.

### 1. Cap the CPU
Stop Polars from grabbing every core:

```python
import os
os.environ["POLARS_MAX_THREADS"] = "4"
```

### 2. Scan, don't read
Never use `pl.read_parquet()` — you don't have enough RAM. Use `scan_parquet()` to build a
**LazyFrame**, which is a *plan* rather than a load:

```python
df_lazy = pl.scan_parquet("data/raw/aisdk-2024-1h.parquet")  # ~instant, loads nothing
```

### 3. Filter early, collect late
Throw away rows and columns *before* bringing anything into memory. Select only what you
need (e.g. `MMSI`, `Latitude`, `Longitude`) instead of all 26 columns.

### 4. The "go" button
Nothing actually runs until you call `.collect()`. If it's still too heavy, stream it in
small sips:

```python
result = df_lazy.filter(...).select(...).collect(streaming=True)
```

### 5. Prototype on a sample
Don't run your full logic on 100M rows every iteration. Test on a sample first:

```python
sample = df_lazy.head(100_000).collect()
```
