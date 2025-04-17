---
cwd: .
runme:
  id: 01JRYZYW1230QTEY7CP58DFD62
  version: v3
shell: dagger shell
terminalRows: 20
---

### ビルド

以下のDagger Shellを実行するとViteのビルドが実行されます。

```sh {"id":"01JRZ01FNXFN9XABZYVY3SPS4B","terminalRows":"18","vsls_cell_id":"317b8357-1fd0-4aa3-96aa-05f3e956e8d3"}
container |
    from node:latest |
    with-exec -- npm install -g pnpm@latest |
    with-directory /src . --exclude node_modules | # node_modulesは除外する
    with-workdir /src |
    with-exec pnpm install |
    with-exec pnpm run build |
    directory ./dist |
    export ./dist
```

### 型＆lintチェック

以下のDagger Shellを実行すると型＆lintチェックが実行されます。

```sh {"vsls_cell_id":"f85369d6-2718-49ae-b2df-68214bfc79ae"}
container |
    from node:latest |
    with-exec -- npm install -g pnpm@latest |
    with-directory /src . --exclude node_modules | # node_modulesは除外する
    with-workdir /src |
    with-exec pnpm install |
    with-exec -- pnpm run ts:check |
    with-exec -- pnpm run lint
```

### pnpmのバージョン確認

以下のDagger Shellを実行するとpnpmのバージョンが出力されます。

```sh
container |
    from node:latest |
    with-exec -- npm install -g pnpm@latest |
    with-directory /src . --exclude node_modules | # node_modulesは除外する
    with-workdir /src |
    with-exec pnpm install |
    with-exec -- pnpm --version |
    stdout
```