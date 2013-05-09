gen-oath-safe script creates appropriate keys and QR codes for setting
up custom tokens for LinOTP.  It can create TOTP (time based) and HOTP
(event based) tokens, and provide textmode QR codes for loading into
Google Authenticator.  It can also provide the needed commands to
prepare a Yubikey.

Requires: python, openssl, qrencode, caca-utils
