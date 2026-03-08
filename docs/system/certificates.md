# HTTPS Certificates

WROLPi uses HTTPS to secure connections between your devices and your WROLPi. Because WROLPi is designed for offline
use, it cannot use a public certificate authority like Let's Encrypt. Instead, WROLPi generates its own **Root CA
certificate** which you install once on each device that connects to it.

## Why HTTPS?

HTTPS encrypts traffic between your browser and WROLPi. Without it, anyone on your local network could intercept
passwords, files, or other data in transit. Many modern browser features also require HTTPS to function. The Kiwix
browser requires HTTPS for some media to load.

## How It Works

WROLPi uses a two-level certificate system:

1. **Root CA** — A long-lived certificate authority stored on the WROLPi media drive. This is generated once and never
   changes. You install this on your devices so they trust your WROLPi.
2. **Leaf certificate** — A short-lived server certificate signed by the Root CA. This is regenerated automatically
   when your WROLPi's hostname or IP address changes. Because your devices already trust the Root CA, they will
   automatically trust any new leaf certificate.

## Downloading the Root CA Certificate

You can download the Root CA certificate from:

* The HTTP landing page at `http://<your-wrolpi-address>/` (or `http://<your-wrolpi-address>:8080/` for Docker)
* The Settings page in the WROLPi interface under **Configs**
* Directly at `http://<your-wrolpi-address>/ca.crt`

## Installing the Certificate

After downloading the `wrolpi-ca.crt` file, follow the instructions for your device:

### iOS / iPadOS

1. Tap the download link, then tap **Allow** when prompted.
2. Open **Settings** > **General** > **VPN & Device Management**.
3. Tap **WROLPi Root CA** > **Install** > enter your passcode.
4. Go to **Settings** > **General** > **About** > **Certificate Trust Settings**.
5. Enable full trust for **WROLPi Root CA**.

### Android

1. Tap the download link.
2. Open **Settings** > **Security & privacy** > **More security settings** > **Encryption & credentials** > **Install
   a certificate** > **CA certificate**.
3. Select the downloaded `wrolpi-ca.crt` file and confirm.

> Menu paths vary by manufacturer. If you can't find it, search for "certificate" in Settings.

### macOS

1. Double-click the downloaded `wrolpi-ca.crt` file to open Keychain Access.
2. Add it to the **System** or **login** keychain.
3. Find **WROLPi Root CA** in the keychain, double-click it.
4. Expand **Trust**, set *When using this certificate* to **Always Trust**.
5. Close and enter your password to confirm.

### Windows

1. Double-click the downloaded `wrolpi-ca.crt` file.
2. Click **Install Certificate** > **Local Machine** > **Next**.
3. Select **Place all certificates in the following store** > **Browse** > **Trusted Root Certification Authorities**.
4. Click **Finish**.

### Linux (Debian / Ubuntu)

1. Copy the certificate: `sudo cp wrolpi-ca.crt /usr/local/share/ca-certificates/`
2. Update the trust store: `sudo update-ca-certificates`
3. Restart your browser. Chromium-based browsers (Chrome, Edge) will use the system store automatically.

> Firefox on Linux does _not_ use the system trust store by default — see the Firefox section below.

### Firefox (all platforms)

Since Firefox 120, Firefox **automatically trusts** root certificates installed in the OS certificate store on
**Windows, macOS, and Android**. If you've already installed the certificate above, Firefox should work with no extra
steps on those platforms.

On **Linux** (or if auto-trust is disabled), import manually:

1. Open Firefox, go to **Settings** > **Privacy & Security**.
2. Scroll to **Certificates** > click **View Certificates**.
3. In the **Authorities** tab, click **Import**.
4. Select the downloaded `wrolpi-ca.crt` file.
5. Check **Trust this CA to identify websites** > **OK**.

> Alternatively, enable auto-trust: go to `about:config` and set `security.enterprise_roots.enabled` to `true`.

## Security: Man-in-the-Middle (MITM) Mitigation

When you install a Root CA on your device, you are trusting it to vouch for the identity of servers. A compromised or
malicious CA could sign certificates for _any_ domain, allowing an attacker to impersonate websites and intercept your
traffic. This is a man-in-the-middle (MITM) attack.

WROLPi mitigates this risk with **Name Constraints**. The Root CA certificate includes a critical `nameConstraints`
extension that restricts which domains and IP addresses it is allowed to sign certificates for. Specifically, the
WROLPi Root CA can **only** sign certificates for:

* `localhost` and `.local` hostnames
* Private/local IP ranges:
    * `127.0.0.0/8` (loopback)
    * `10.0.0.0/8` (private)
    * `172.16.0.0/12` (private)
    * `192.168.0.0/16` (private)
    * `::1` (IPv6 loopback)
    * `fc00::/7` and `fe80::/10` (IPv6 private and link-local)

This means that even if someone obtained the WROLPi Root CA private key, they **could not** use it to create fake
certificates for public websites like `google.com` or `your-bank.com`. Your browser would reject any such certificate
because it violates the name constraints. The WROLPi Root CA is only valid for local network addresses — exactly where
your WROLPi lives.

This is a defense-in-depth measure. The Root CA private key is stored on your WROLPi's media drive and never leaves the
device.
