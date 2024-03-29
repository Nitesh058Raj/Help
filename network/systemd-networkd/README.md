# Static IP Configuration using systemd-networkd

This guide provides step-by-step instructions for configuring a static IP address using systemd-networkd on a Unix-based operating system.

## Prerequisites

- Unix-based operating system (e.g., Linux, macOS)
- Root or sudo access

## Steps

1. Open the terminal and navigate to the network configuration directory:
   ```bash
   cd /etc/systemd/network/
   ```

2. Determine the names of the network interfaces you want to configure. You can use the `ip addr` or `ifconfig` command to list all network interfaces along with their current configurations.

3. Create a new configuration file for the network interface. For example, if you want to configure the eth0 interface, create a file named 10-static-eth0.network:

    ```bash
    sudo vi 10-static-eth0.network
    ```

4. In the configuration file, add the following content to set the static IP address, gateway, and DNS servers:

    ```bash
    [Match]
    Name=eth0

    [Network]
    Address=192.168.1.100/24
    Gateway=192.168.1.1
    DNS=8.8.8.8
    DNS=8.8.4.4
    ```

5. Save the configuration file and exit the text editor.

6. Restart the systemd-networkd service to apply the changes:
    ```bash
    sudo systemctl restart systemd-networkd
    ```
    OR
    ```bash
    sudo systemctl reboot
    ```

7. Verify the static IP configuration by checking the network interface status:
    ```bash
    ip addr show eth0
    ```
    OR
    ```bash
    ifconfig eth0
    ```

## Additional Resources

   - [systemd-networkd documentation](https://www.freedesktop.org/software/systemd/man/systemd.network.html)
   - [systemd documentation](https://www.freedesktop.org/software/systemd/man/systemd.html)

## Conclusion

That's it! You have successfully configured a static IP address using systemd-networkd.

