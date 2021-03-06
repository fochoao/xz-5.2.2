## README For xz 5.2.2 and LZMA2 compression and de-compression of files based on lzma or 7 zip.

# Compiled for Windows 10 in x86 and x64.


XZ Utils
========

    0. Overview
    1. Documentation
       1.1. Overall documentation
       1.2. Documentation for command-line tools
       1.3. Documentation for liblzma
    2. Version numbering
    3. Reporting bugs
    4. Translating the xz tool
    5. Other implementations of the .xz format
    6. Contact information


0. Overview
-----------

    XZ Utils provide a general-purpose data-compression library plus
    command-line tools. The native file format is the .xz format, but
    also the legacy .lzma format is supported. The .xz format supports
    multiple compression algorithms, which are called "filters" in the
    context of XZ Utils. The primary filter is currently LZMA2. With
    typical files, XZ Utils create about 30 % smaller files than gzip.

    To ease adapting support for the .xz format into existing applications
    and scripts, the API of liblzma is somewhat similar to the API of the
    popular zlib library. For the same reason, the command-line tool xz
    has a command-line syntax similar to that of gzip.

    When aiming for the highest compression ratio, the LZMA2 encoder uses
    a lot of CPU time and may use, depending on the settings, even
    hundreds of megabytes of RAM. However, in fast modes, the LZMA2 encoder
    competes with bzip2 in compression speed, RAM usage, and compression
    ratio.

    LZMA2 is reasonably fast to decompress. It is a little slower than
    gzip, but a lot faster than bzip2. Being fast to decompress means
    that the .xz format is especially nice when the same file will be
    decompressed very many times (usually on different computers), which
    is the case e.g. when distributing software packages. In such
    situations, it's not too bad if the compression takes some time,
    since that needs to be done only once to benefit many people.

    With some file types, combining (or "chaining") LZMA2 with an
    additional filter can improve the compression ratio. A filter chain may
    contain up to four filters, although usually only one or two are used.
    For example, putting a BCJ (Branch/Call/Jump) filter before LZMA2
    in the filter chain can improve compression ratio of executable files.

    Since the .xz format allows adding new filter IDs, it is possible that
    some day there will be a filter that is, for example, much faster to
    compress than LZMA2 (but probably with worse compression ratio).
    Similarly, it is possible that some day there is a filter that will
    compress better than LZMA2.

    XZ Utils doesn't support multithreaded compression or decompression
    yet. It has been planned though and taken into account when designing
    the .xz file format.
