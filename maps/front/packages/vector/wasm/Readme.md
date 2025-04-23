# Wasm

Wasm is used to satisfy performance requirements in those parts of application where it makes sense, e.g.
tile content decoding (js-wasm communication is minimal, quite a lot work to be done).

### Development
For now browser is not the best debugging environment for compiled wasm (no source maps, no break points,
yet console printing is available). It is much better to run the same code in native platform, using
all the tools available for editing and debugging. That is why there are two main targets for tile decoder
in cmake build setup: **tile_decoder_test** and **tile_decoder.js**.

### Building
```
cmake -B<out_path> -H$<src_path> [-DTARGET_ENV=Native|WASM] [-DCMAKE_BUILD_TYPE=Debug|Release]
cmake --build <out_path>
```

