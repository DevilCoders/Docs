## Frontend server

Project for create proxy/handlers for b2bgeo frontend services

---

Run dev mode - `npm run dev`

Build - `npm run build`

Start compiled project - `npm run start`

---

### Whats needed?

#### 1. YAV_TOKEN

- Add the `YAV_TOKEN` variable to .env file ([Link to get YAV_TOKEN](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982))

- Example (in your .env file)

```sh
YAV_TOKEN=_mOckYavTOKen
```

#### 2. Get secrets

- Run `npm run get-secrets` (This will keep the secret of the service in .env)

#### 3. Setup tvm

- Run `npm run local-tvm` (Creates files for tvm operation,for example `.tvm.json`)

_`Pay attention!`_

In cases where in the file `.tvm.json` in `"secrets":` instead of your token, it says `undefined`, you need to manually register the token in `.env`, that can be taken from [HERE](https://yav.yandex-team.ru/?search=tvm.secret). You must select the secret that corresponds to the value in the `"self_tvm_id:"` field in the `.tvm.json` file and add it to .env, for example

```sh
TVM_CLIENT_SECRET=yoUrTVmSecrEt_
```

After that, you should see in the console the message

```sh
[TVP][INFO]: Started the HTTP-interface (main): [127.0.0.1]:5000
```

If so, you can press `CTRL+C` and go to the next step

#### 4. Run `npm run dev`

### P.S.

You can check how it works, log data, make fixes without running rml, just make the request you need via `postman` or analogues at the url `127.0.0.1/${yourRequest}`

### OAuth token for blackbox-test.yandex.net:
1. Log in https://passport-test.yandex.ru/;
3. Get token via link:
   https://oauth-test.yandex.ru/authorize?response_type=token&client_id=ad4d7e708ef045edbac8ecf7f28015f0

