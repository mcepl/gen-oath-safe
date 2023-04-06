gen-oath-safe
=============

Create OTP secrets, uri, qrcodes, configurations for TOTP and HOTP
authentication.

::

   Licensed under the MIT License <https://mit-license.org/>

   Copyright (C) 2013 Richard Monk <rmonk@redhat.com>
   Copyright (C) 2013-2014 Matěj Cepl <mcepl@cepl.eu>
   Copyright (C) 2016 Thomas Zink <tz@uni.kn>

   Permission is hereby granted, free of charge, to any person
   obtaining a copy of this software and associated documentation
   files (the "Software"), to deal in the Software without
   restriction, including without limitation the rights to use,
   copy, modify, merge, publish, distribute, sublicense, and/or
   sell copies of the Software, and to permit persons to whom the
   Software is furnished to do so, subject to the following
   conditions:

   The above copyright notice and this permission notice shall
   be included in all copies or substantial portions of the
   Software.

   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF
   ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED
   TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR
   A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT
   SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
   CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
   OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR
   IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
   DEALINGS IN THE SOFTWARE.

**gen-oath-safe** can create hex and base32 secrets used for TOTP/HOTP
two factor authentication (two-step verification), used in many services
and applications. It can be used both on the server to generate
server-side configuration, and on the client, to generate the
configuration for authenticator apps and hardware tokens.

The script can use an existing hex encoded secret or creates a new
random secret. Based on the secret it produces a otpauth URI to create a
QR code which is print on stdout and which can be scanned by
authenticator apps (like Google Auhtenticator, FreeOTP, Yubico
Authenticator, Aegis Authenticator). The script also outputs the
configuration used by server-side authentication services like Apache
mod_authn_otp, pam_oath, and linOTP/PrivacyIdea. If Yubikey packages are
installed, and a Yubikey is inserted, the configuration can be directly
written to a free slot (for hotp) or the oath module (for totp). If no
Yubikey is inserted, the corresponding commands to program the key are
output on stdout.

Backup your hex secrets safely (e.g. in an encrypted container) to be
able to restore the configurations.

Requirements
------------

-  **xxd**, **base32**: to convert the hexadecimal secret to base32

-  **qrencode** (optional, recommended): to create the qr code from the
   uri and display it on stdout.

-  **yubikey-personalization** (optional): to probe for Yubikey and
   write hotp configuration to the Yubikey slots.

-  **yubikey-manager** (optional): to write totp configuration to the
   Yubikey oath module.

Installation and Usage
----------------------

Install
~~~~~~~

To install simply put ``gen-oath-safe`` into your ``$PATH``. Or run the
following commands:

::

   $ install -Dm755 ./gen-oath-safe /usr/local/bin/gen-oath-safe 
   $ install -Dm644 ./gen-oath-safe.1 /usr/local/man/man1/gen-oath-safe.1

For Arch, there is a package in the AUR:

::

   $ yay -S gen-oath-safe-git

Usage
~~~~~

To output usage and help use:

::

   gen-oath-safe -h

Synopsis:

::

   gen-oath-safe [issuer:]<username>[@domain] [tokentype] [secret]

The ``username`` can either simply be a user, or include the issuer and
domain, e.g. ``github.com:gituser@github.com``.

The ``tokentype`` is either ``totp`` (default) or ``hotp``.

The ``secret`` is a hex encoded OTP secret. If not provided, a random
secret is generated.

References
----------

-  “HOTP: An HMAC-Based One-Time Password Algorithm”
   http://www.ietf.org/rfc/rfc4226.txt
-  “TOTP: Time-Based One-Time Password Algorithm”
   https://www.ietf.org/rfc/rfc6238.txt
-  mod_authn_otp https://github.com/archiecobbs/mod-authn-otp
-  pam_oath https://wiki.archlinux.org/title/Pam_oath
-  linOTP https://linotp.org/
-  Aegis Authenticator https://getaegis.app/
-  FreeOTP https://freeotp.github.io/
-  Yubico Authenticator
   https://www.yubico.com/products/yubico-authenticator/
