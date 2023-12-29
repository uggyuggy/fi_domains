# .fi domain names



## 🎯 Purpose

This repository purpose is to daily share the list of `.fi` domain names. (As I have not found another public share of this list for now)

So people don't have to do it on their side too (as long as list is updated here of course).

(Also less the people run their own scripts on their side, less the remote server will be loaded, possibly the longer the list of domain will remains publicaly available) 





## 🤝 Credits

I found the original informations on how to get those from Jan Schaumann who was also sharing a script on his repo  https://github.com/jschauma/tld-zoneinfo/





## ☕ Sample

```
$ curl -s -L https://github.com/uggyuggy/fi_domains/raw/main/fi.txt -o fi.txt
$
$ wc -l fi.txt
434180 fi.txt
$
$ head fi.txt
# .fi domain names (politely) extracted from https://odata.domain.fi on 31Feb2000 05:57 UTC
0-0-outlet.fi.
0-0.fi.
0-100.fi.
0-koodi.fi.
0-waste.fi.
00.fi.
000.fi.
001.fi.
002.fi.
$
```





## 📰 Informations

- Data is retrieved using Odata interface, as "officially" mentioned on

https://tieto.traficom.fi/en/datatraficom/open-data?toggle=Fi-domain%20names

> The data is also available via the OData  interface.

- Inspired by the Jan Schaumann script , I rewrited my own script, adding few things:

  - Management of some retry/errors
  - Basic checks if the list seems to be full
  - Logs
  - Etc..

  My own script is not shared yet because:

  - I'm shy
  - It's not tested enough over many days yet
  - It would defeat the purpose of sharing the fully built list, to prevent the remote server to be overloaded for same purpose.
  - Jan already shared one

- There is around 434 000 domain names (as the time of writing) 

- The odata.domain.fi HTTPS server seems to reply a maximum of only 100 domain names per request, which means that the script has to send  ~ 4340 queries one by one to get the full list of domain names. (Each request gives the next offset to be requested)
- To be nice with the remote server, my script also does pause 1 second between each of the requests. So the script takes a minimum of 4340 seconds (1 h 12 min) to complete. Which seems fine to me for a daily updated list.
- The file served here should be updated 1 time per day to not overload the remote server for no reason.
- The file contains an additional comment line at the top starting with `#` that contain an UTC date information.
- For now there is a single comment line, but in case I add more in the future, you may better remove everything that start with a `#`
- The domain names end with `.fi.` (added by the script as this is not replied by the remote server).
- The domain names are provided sorted ( `LC_ALL=C sort -u`)
- IDN domain names are converted in their `xn--` version. 
- If there is no domain list provided for a specific day, this could mean my script failed to build/push the list due to:
  - The .fi remote server rejected me / blacklisted me
  - My script was not able to recover from some errors (reminder, it send ~ 4340 queries, so 4340 chances to have problems)
  - The .fi remote server is down
  - My own client server runnig the script is down
  - Github was down :)
  - Network issue, DNS issue ...
  - ...
- You should be able to guess if the file has been updated successfully by checking either:
  - The date into the first comment line. `LC_TIME=C date -u +'%d%b%Y %H:%M UTC'`
  - The date of the last Github commit





## 🚧 Todo

- [x] Write README
- [x] Add emojis to the README (very important 🚨)

- [ ] Find when (if there one specific) that is updated on the domain.fi server (and run the script at the right time)

- [ ] Add more warning notifications in case of script failures
- [ ] Add more control to guess if something went wrong with script
- [ ] What happens if the remote server update the list in the middle of my running script (aka `odata.count` we got at the very beginning and used as one control at the end, does not match anymore the number of domains returned   )
- [ ] Change UserAgent to give clue to the .fi remote server who am I so they could contact me 
- [ ] After I will be confident it's running as expected, possibly informing Jan
- [ ] ...

