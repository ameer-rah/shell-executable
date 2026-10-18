# shell-executable

A minimal TCP **reverse shell** written in C for POSIX systems (macOS/Linux), built as a learning exercise in network and systems programming. When run, the program opens a TCP connection *back* to a listener you control, wires an interactive `/bin/sh` to that connection, and lets you run commands over the socket. The outbound connection is what makes it a *reverse* shell (as opposed to a bind shell that waits for an incoming connection).

> ⚠️ **For education and authorized testing only.** Use this only on systems you own or have explicit, written permission to test. Running a reverse shell against machines you don't control is illegal in most jurisdictions. You are responsible for how you use it.

## How it works
The program does five things:
1. **`socket()`** — create a TCP socket.
2. **`inet_pton()` + `sockaddr_in`** — build the listener's address from the IP and port arguments.
3. **`connect()`** — dial out to the listener.
4. **`dup2()` ×3** — redirect `stdin`, `stdout`, and `stderr` onto the socket.
5. **`execl()`** — replace the process with an interactive `/bin/sh`.

> On a fresh macOS install you may first need to accept the Xcode command-line-tools license: `sudo xcodebuild -license`.

## License
MIT