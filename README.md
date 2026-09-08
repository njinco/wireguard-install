# WireGuard Install Fork

A small fork of [hwdsl2/wireguard-install](https://github.com/hwdsl2/wireguard-install) for installing and managing a WireGuard VPN server.

## Changes in this fork

- Added an interactive **Update server address** option to the existing-install menu.
- Added `--updatedomain [DNS name or IP]`.
- Added interactive and command-line client DNS updates with `--updatedns`.
- Updates existing client profiles to use the new endpoint without changing their keys or VPN addresses.
- Creates a timestamped backup in the directory where the script is run before changing configuration files.
- Supports updating older installations that use the original script’s configuration format.

## Download and install

Download this fork on the VPN server:

```bash
curl -fL -o wireguard.sh https://raw.githubusercontent.com/njinco/wireguard-install/master/wireguard-install.sh
chmod +x wireguard.sh
```

Install WireGuard:

```bash
sudo bash wireguard.sh
```

## Update an existing server address

Run the script and select:

```text
5) Update server address
```

Or use the command line. Omitting the address starts an interactive prompt:

```bash
sudo bash wireguard.sh --updatedomain
```

You can also provide the address directly:

```bash
sudo bash wireguard.sh --updatedomain vpn.example.org
```

Before updating, the script creates a backup such as:

```text
./domain-update-backup-YYYYMMDD-HHMMSS/
```

Existing client `.conf` files are updated in place. Re-import them into WireGuard, or display an updated QR code with:

```bash
sudo bash wireguard.sh --showclientqr client-name
```

Make sure the new DNS record points to the VPN server before updating the client profiles.

## Update client DNS

Run the script and select:

```text
6) Update client DNS
```

Or use the command line:

```bash
sudo bash wireguard.sh --updatedns
sudo bash wireguard.sh --updatedns 1.1.1.1 1.0.0.1
```

This updates existing client profiles and creates a `dns-update-backup-YYYYMMDD-HHMMSS` backup.

## License and credits

This fork is distributed under the MIT License. It retains the original copyright notices required by the license:

- Lin Song, 2022–2026
- Nyr, 2020–2023

See [LICENSE.txt](LICENSE.txt) for the complete license text. The original project is available at [hwdsl2/wireguard-install](https://github.com/hwdsl2/wireguard-install).
