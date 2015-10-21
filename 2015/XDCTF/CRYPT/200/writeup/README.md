首先查看程序，可以发现这题其实就两个操作，mkprof 是将所给字符串加上前后缀后加密，parse 是将所给加密的串解密，只要串中含有一个特定子串（加密的时候不能输入含有这个子串的串）就能拿到 flag。

而这里的加密采取分段的方式，每一段将当前段明文与前一段的密文异或的结果用一个固定的我们不知道的 key 来进行 AES 加密。

那么对于两个串 A 和 B，我们首先拿到 A 的第 n 段和 B 的第 n 段的加密结果（要求两者不一样），然后我们在 B 的第 n+1 段中含有所需特定字符串，由于我们不能直接要求服务器对 B 进行加密，我们可以将 A 的第 n+1 段设为一个特定的字符串，满足此串与 A 的第 n 段加密结果异或的值和 B 的第 n+1 段明文与 B 的第 n 段的加密结果异或的值一样，那么显然此时 A 与 B 第 n+1 段加密出来的结果会是一样的。于是我们将 A 加密得到的第 n+1 段拼在 B 的前 n 段的加密结果后面去解密，就能通过判断，拿到 flag。