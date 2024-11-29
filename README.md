## moshi-swift

This repo contains an experimental implementation of
[mimi](https://huggingface.co/kyutai/mimi) and
[moshi](https://github.com/kyutai-labs/moshi) using [MLX
Swift](https://github.com/ml-explore/mlx-swift).

```bash
xcodebuild -scheme moshi-cli -derivedDataPath ./build
./build/Build/Products/Release/MoshiCLI moshi-7b ~/tmp/ model.q4.safetensors
```

### Downloading the checkpoints and test data
```bash
wget https://huggingface.co/kyutai/moshika-candle-bf16/resolve/main/tokenizer-e351c8d8-checkpoint125.safetensors
wget https://huggingface.co/kyutai/moshiko-mlx-q4/resolve/main/model.q4.safetensors
wget https://github.com/metavoiceio/metavoice-src/raw/main/assets/bria.mp3
ffmpeg -i bria.mp3 -ar 24000 bria-24khz.mp3
```
Move all the asset files in `~/tmp`.

### Possible workarounds for common issues
`LD_RUNPATH_SEARCH_PATHS` has been set in xcode to include the executable path
which is where the `moshi-lib` framework seems to be compiled.

When running on the command line via ssh, this may require unlocking the keychain with:
```
security unlock-keychain
```

Added to `OTHER_SWIFT_FLAGS` `-no-verify-emitter-module-interface`,
as per [github issue](https://github.com/swiftlang/swift/issues/64669).


