Pandas

DuckDB

Arrow
    ~~Does Arrow handle larger than memory datasets transparently.~~
    Arrow is an **in-memory data format**. It's a columnar format that supports all kinds of data types and it's been designed with the goal of zero-copy reads from multiple processes, eliminating serialization/deserialization overhead. It is also built for modern hardware, considering vectorization and SIMD for CPU and memory-efficient data analysis workloads.
    It has been adopted already by so many projects, using its bindings for many programming languages
    They also designed a binary protocol for IPC using shared memory. But I'm not sure what could that be for, maybe for concurrent data analysis?



GeoArrow + GeoParquet



Reference Links:
https://duckdb.org/2023/03/03/json.html
https://github.com/markfairbanks/tidypolars#tidypolars
https://github.com/pola-rs/polars
https://arrow.apache.org/docs/
https://waterprogramming.wordpress.com/2022/03/07/efficient-storage-and-querying-of-geospatial-data-with-parquet-and-duckdb/