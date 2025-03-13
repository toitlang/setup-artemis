# Artemis GitHub runner

Setup instructions for setting up the self-hosted x64 GitHub
runner.

## Hardware
Connect an ESP32 dev-board to the machine. Pins 32 and 33 should be
connected to each other.

Update the 99-usb-uart-artemis.rules file and copy it to
`/etc/udev/rules.d/`.

Reload and restart as follows:
```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

You should have a /dev/ttyArtemis device now.

## Test env file

The `artemis-test.env` file is read by the workflow to
get the local configuration.

Adjust the `artemis-test.env` file and copy it to your home.

## GitHub runner

Register this machine as a GitHub action runner in the
https://github.com/toitware organization. Use the directory
`actions-runner-toitware` instead of `actions-runner'.
https://github.com/organizations/toitware/settings/actions/runners/new

Add the `serial-artemis` label to the runner.

Automatically run the runner at boot.
https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/configuring-the-self-hosted-runner-application-as-a-service

```bash
# In the 'actions-runner-toitware' folder:
sudo ./svc.sh install
sudo ./svc.sh start
sudo ./svc.sh status
```
