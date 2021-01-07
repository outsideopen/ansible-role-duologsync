# ansible-role-duologsync

Installs Duo log sync package for Python.

## Role Variables

| Variable                           | Default | Comments                                        |
| :--------------------------------- | :------ | :---------------------------------------------- |
| duologsync_path                    | /opt/duologsync | The path to install the duologsync              |
| duologsync_systemd_path            | /etc/systemd/system | The path to for the systemd service file        |
| duologsync_install_os_dependencies | true | Whether or not to install OS level dependencies. Set this to `false` when you want to manage the dependencies on your own |
| duologsync_install_setuptools      | true | Whether or not `setuptools` should be installed |
| duologsync_update_apt_cache        | true | Whether or not to update the APT cache (Debian/Ubuntu Only |
| duologsync_repo_url                | https://github.com/duosecurity/duo_log_sync | The URL to the Duo log sync repository |
| duologsync_user                    | duologsync | The user to run duologsync as |
| duologsync_group                   | duologsync | The group to run duologsync as |
| duologsync_integration_key         | | The Integration key |
| duologsync_private_key             | | The Private key |
| duologsync_api_hostname            | | The api-hostname of the server hosting this account's logs. Show in the Duo admin panel |
| duologsync_servers                 | | Define how the logs should be sent. See below for the format |
| duologsync_account_is_msp          | | Whether the Duo account is a Duo MSP account with child accounts |

### duologsync_servers

The valid endpoints are defined the duo_log_sync [template_config.yml](https://github.com/duosecurity/duo_log_sync/blob/master/template_config.yml#L120) file.

Note: the `duologsync_log_format` is a global option, so set up the servers according to using `CEF` or `JSON`.

```yaml
duologsync_servers:
  - id: graylog
    hostname: graylog.example.com
    port: 5151
    protocol: UDP
    endpoints:
      - adminaction
      - auth
      - telephony
      - trustmonitor
```

## Testing

Testing requires Molecule and Docker

```
pip3 install -r requirements.txt
molecule test
```

## License

MIT