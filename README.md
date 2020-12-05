# hunter2
A minimalist password manager

## Concept:

- It's a password manager that doesn't need a chrome plugin, or an `.exe` run as administrator.
- It uses the lingua franca of devices with browsers - JS.
- Passwords are encrypted with AES256-CTR, the nonce increments on reset.
- Everything is packed into one HTML file with a block of JS at the top containing the password DB.
- Any modifications [generate a new HTML file][1]
    - alternatively a block of JS is shown
        - can be manually appended to the JS DB for new entries
        - or replace an existing entry.

```
  argon2di(pass,salt,len=256)+--+
                                |
+------------------+ aes-256(   |
|                  |   nonce,   |
| +-Master:------+ |   key)<----+
| |*************…| |
| +--------------+ |
|                  |
| +-Authority:---+ |
| |gmail.com     | |
| +--------------+ |
| +-Plaintext:---+ |
| |hunter2       | |
| +--------------+ |
| +-Ciphertext:--+ |
| |n=1;qyLq5iQ+V…| |
| +--------------+ |
|                  |
| +-Authority:---+ |
| |github.com    | |
+------------------+
```

Entering plaintext and submitting increments the nonce at the beginning of the ciphertext
Entering a master password creates a Decrypt button next to each block
Argon's parameters are tuned to the oldest functional smartphone I can find (an S2) to use maximum memory and take ~8s to decrypt. These can be changed and saved as advanced parameters.

## TODO
- [x] Fix ugly README diagram - GitHub has some non-monospace font preferences
- [ ] textarea height 100% not working
- [ ] Use ROT13 for demo
- [ ] [argon2 js](https://en.wikipedia.org/wiki/Argon2)
- [ ] [AES JS](https://en.wikipedia.org/wiki/AES_implementations#JavaScript)

[1]: https://tiddlywiki.com/ "looks to have implemented something very similar, should look into their approach."
