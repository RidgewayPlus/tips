# Fixing issues with TP‐Link routers and your SIP trunks not being able to register.

### This targets an issue where when you look at the logs of your FreePBX server, it shows something along the lines of "No response recieved on registration attempt". I was faced with this issue after switching from an Asus Router back to a TP-Link router

## Router used: TP-Link Archer AX10/AX1500 connected to the internet via Superloop FTTP

## Connect to your FreePBX server over SSH
`ssh user@server_ip`

## Open `/etc/asterisk/pjsip.transports_custom.conf` with your text editor of choice. 
### For me, this file was empty when I opened it.

## Add the following lines
`[0.0.0.0-udp](+)
rewrite_contact = yes
force_rport = yes`

## Save changes to the file, then run `fwconsole restart`
### If it shows command not found then run it again using `sudo`

## Check your registrations
### Check your registrations by running `sudo rasterisk`, then running `pjsip show registrations`
### If it now shows Registered, congrats you have fixed your issue. 
