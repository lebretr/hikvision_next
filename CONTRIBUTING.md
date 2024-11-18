## Linting

- Install Ruff extension and select ruff as default formatter in vscode settings
- Code must follow [Home Assistant code style guidelines](https://developers.home-assistant.io/docs/development_guidelines)
- Line length limit must be 120 characters

## Testing

There are 2 types of tests:

### ISAPI communication
They test specific ISAPI requests and uses data from `fixtures/ISAPI`. They are focued on data processing. The folder structure corresponds to ISAPI endpoints, and the XML files contain device responses.

### The behavior of the device in HomeAssistant

They initialize the entire device in the HomeAssistant environment and uses data from `fixtures/devices`. Each JSON file contains all the responses to GET requests sent by the given device.

They can be recorded for any device in the Device Info window by clicking DOWNLOAD DIAGNOSTICS button. All sensitive data such as MAC addresses, IPs, and serial numbers are anonymized so they can be safely made public.

This approach should make it easier to develop this integration for an even greater number of devices without the need for physical access to the device.

### Testing on windows

If you develop on windows, there are some limits with pytest-homeassistant-custom-component when you want to run the unit tests

See this [issue](https://github.com/MatthewFlamm/pytest-homeassistant-custom-component/issues/154) for more detail.

The simplest way is to use docker on your PC:
- Install [docker](https://docs.docker.com/desktop/setup/install/windows-install/)
- next, in a cmd window:
```
REM go to the hikvision_next directory. example:
cd C:\Users\john\Documents\github\hikvision_next

REM Build a docker container 
docker build -f run_test.dockerfile -t mine/pytest-homeassistant-custom-component:latest .

REM Clear console and Run test in your container
cls && docker run --rm -v .:/app mine/pytest-homeassistant-custom-component:latest
```