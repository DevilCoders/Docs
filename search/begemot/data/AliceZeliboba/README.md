# Zeliboba inference for Alice
See https://st.yandex-team.ru/ZELIBOBA-466.

Build with right CUDA flags:
```bash
ya make -r --checkout --yt-store . $SHARD $FRESH -j32 -DCUDA_VERSION=11.4 -DCUDNN_VERSION=8.0.5
```