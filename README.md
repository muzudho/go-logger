# go-logger

Loging library.

## Set up

```shell
go build
```

## Usage

```go
	// Working directory
	wd, err := os.Getwd()
	if err != nil {
		panic(err)
	}

	tracePath := filepath.Join(wd, "output/trace.log")
	debugPath := filepath.Join(wd, "output/debug.log")
	infoPath := filepath.Join(wd, "output/info.log")
	noticePath := filepath.Join(wd, "output/notice.log")
	warnPath := filepath.Join(wd, "output/warn.log")
	errorPath := filepath.Join(wd, "output/error.log")
	fatalPath := filepath.Join(wd, "output/fatal.log")
	printPath := filepath.Join(wd, "output/print.log")

	// ロガーの作成。ディレクトリが存在しなければ、強制終了してしまいます
	log = *NewLogger(
		tracePath,
		debugPath,
		infoPath,
		noticePath,
		warnPath,
		errorPath,
		fatalPath,
		printPath)

	// 既存のログ・ファイルを削除
	log.RemoveAllOldLogs()

	// ログ・ファイルの開閉
	err = log.OpenAllLogs()
	if err != nil {
		// ログ・ファイルを開くのに失敗したのだから、ログ・ファイルへは書き込めません
		panic(err)
	}
	defer log.CloseAllLogs()

	log.Trace("Hello, world!!\n")

	// チャッターの作成。 標準出力とロガーを一緒にしたラッパーです
	chat = *NewChatter(log)
	stderrChat = *NewStderrChatter(log)

	chat.Trace("Hello, Japan!!\n")
	stderrChat.Trace("Hello, Saitama!!\n")
}
```
