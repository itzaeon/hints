The following commands allow me to connect to an `802-1x` secured network.

```bash
nmcli connection add \
> type wifi con-name "BYOD" ifname wlp3s0 ssid "BYOD" -- \
> wifi-sec.key-mgmt wpa-eap 802-1x.eap ttls \
> 802-1x.phase2-auth mschapv2 802-1x.identity "rathn"
```

After, open `nmtui` (requires the `networkmanager` package) and connect using your credentials.
