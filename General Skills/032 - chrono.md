# Descripcion
How to automate tasks to run at intervals on linux servers?
## Solucion
 `picoplayer@challenge:~$ crontab -l`
`no crontab for picoplayer`
`picoplayer@challenge:~$ crontab -e`
`no crontab for picoplayer - using an empty one`
`update-alternatives: error: no alternatives for editor`
`/usr/bin/sensible-editor: 25: editor: not found`
`/usr/bin/sensible-editor: 28: nano: not found`
`/usr/bin/sensible-editor: 31: nano-tiny: not found`
`/usr/bin/sensible-editor: 34: vi: not found`
`Couldn't find an editor!`
`Set the $EDITOR environment variable to your desired editor.`
`crontab: "/usr/bin/sensible-editor" exited with status 1`
`picoplayer@challenge:~$ crontab -u root -l`
`must be privileged to use -u`
`picoplayer@challenge:~$ sudo -l`
`[sudo] password for picoplayer:` 
`Sorry, user picoplayer may not run sudo on challenge.`
`picoplayer@challenge:~$ cat /etc/crontab`

## Notas Adicionales
+ crontab contenia la bandera y habia que aplicar un cat , esto porque era un archivo de configuracion
## Referencias
+ https://github.com/snwau/picoCTF-2023-Writeup/blob/main/General%20Skills/chrono/chrono.md

