// FORENSIC REPORT.


First Step : 

```console
  vol -f ~/EPITECH/POC/cyber-forensic-Keuchnotkush/vmss.core windows.sessions.Sessions
```
  While analyzing the output, we identiied two users : PoC{BrunoDeChezPoC,PoC_W0rk$Hop}.

  
Second Step :
  
  we had to analyze traffic around https://www.poc-innovation.fr/.
  To do so we ran at netscan on the vmss.core file :
  ```console
    vol -f ~/EPITECH/POC/cyber-forensic-Keuchnotkush/vmss.core windows.netscan.netscan
  ```
The output ended up being a bit large but i noticed https connections through python.exe.
  So i decided to grep port 443 and python.exe and i identified the flag : PoC{7912 + python.exe}

Third Step :

  I ran :
  ```console
  vol -f ~/EPITECH/POC/cyber-forensic-Keuchnotkush/vmss.core cmdline --pid=7912
  ```
  To get the following output :
  ```console
    7912	python.exe	C:\Users\BrunoDeChezPoC\AppData\Local\Programs\Python\Python38\python.exe BadProgram.py.txt
  ```
  PoC{7881be27f7507725dc5229f5700f36a7cacc1fb0}

Fourth Step :

  I ran :
  ```console
  vol -f ~/EPITECH/POC/cyber-forensic-Keuchnotkush/vmss.core -o ~/volatility3/ windows.memmap.Memmap --pid 7912 --dump
  ```
  Flag is : PoC{a159a032804f3fc6e9d7d9310ea882aa9b176025d09920e4f847761d0411ca1d51fbffe9e4bf9920ce98eaafedcf789fb235932bb8e6cf8ecd7a5730202636bd}
