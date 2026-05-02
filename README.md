# TryHackMe_LianYu
Start with a scan: `Nmap -sC -sV 10.48.144.254`
<img width="730" height="481" alt="Screenshot 2026-05-02 112618" src="https://github.com/user-attachments/assets/a13a497b-5c56-476e-98bf-dcd8e45ed79d" />
<img width="758" height="499" alt="Screenshot 2026-05-02 112633" src="https://github.com/user-attachments/assets/f36ce475-3dc6-4197-ba31-26a651d4dc36" />
This picture shows ssh and ftp service is existed in this IP.
There apache(web): `http://10.48.144.254`
Just a blog about Arrowverse

Use 'Gobuster' to discover hidden directories and files on a web server. 
When you visit a website normally, you only see pages that are linked in the UI, but many servers contain unlisted or hidden paths

Next step, try to check for a hidden directory using: 'gobuster dir --url 10.48.144.254 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt'
<img width="748" height="437" alt="Screenshot 2026-05-02 113236" src="https://github.com/user-attachments/assets/b54806f2-48f8-4101-9512-1a347d417c27" />

Use `Inspect Element` by pressing F12 to see if there's any hidden Text
<img width="690" height="734" alt="Screenshot 2026-05-02 113337" src="https://github.com/user-attachments/assets/4f35fbf8-ae8c-41cf-a1c4-6cb5cd0be670" />
Found Hidden Word probally for something

Add `/island` inside previous Gobuster so we can see what inside that Webpage
``gobuster dir --url 10.48.144.254/island --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt``
<img width="770" height="418" alt="Screenshot 2026-05-02 113546" src="https://github.com/user-attachments/assets/6b6bbc07-1103-423d-83b5-396bf59a58af" />
Found '/2100' Hidden Page

<img width="875" height="568" alt="Screenshot 2026-05-02 113634" src="https://github.com/user-attachments/assets/878cf35c-b2e6-406f-9267-26b7e606b3fa" />

The other method from `Inspect Element` is `View Page Source`
<img width="875" height="568" alt="Screenshot 2026-05-02 113634" src="https://github.com/user-attachments/assets/5c0d1fd2-92e2-4b89-b886-65ae5f4070f0" />

<img width="728" height="416" alt="Screenshot 2026-05-02 113642" src="https://github.com/user-attachments/assets/b3c19fb9-00ca-4870-9f3d-87039183caf1" />
It shows there's nothing inside the page but it shows ".ticket."

Try ``gobuster dir --url 10.48.144.254/island/2100 --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x.ticket``
why -x .ticket?
-x = extension || while .ticket indicates: “Also try each word in the wordlist with .ticket added at the end"
<img width="740" height="415" alt="Screenshot 2026-05-02 113937" src="https://github.com/user-attachments/assets/fcf63beb-2388-48d2-8ac7-7890137f4eff" />

Then go to `green_arrow.ticket`
<img width="723" height="252" alt="Screenshot 2026-05-02 114208" src="https://github.com/user-attachments/assets/bfddff2c-991e-45df-858e-7b7e34fd0c4a" />
It shows some kind of Code we use 'Base58 Decode' To findout the secret code
<img width="614" height="498" alt="Screenshot 2026-05-02 114339" src="https://github.com/user-attachments/assets/049727a0-eb84-4a0b-a04e-02f6f0c7c785" />
Now got the secret code we want to get.
First get `Vigilante` and now `!#th3h00d`
Then try to enter FTP which is `ftp 10.48.144.254`
then enter username Vigilante and the pass
<img width="425" height="203" alt="Screenshot 2026-05-02 114609" src="https://github.com/user-attachments/assets/062735f0-8b66-4a64-894b-778f712d56e4" />
After that do `ls -a` to List all the item inside
<img width="698" height="255" alt="Screenshot 2026-05-02 114639" src="https://github.com/user-attachments/assets/9a7390e3-4c26-40c3-8367-2a68cc72884a" />
Do `get` to get items
<img width="715" height="387" alt="Screenshot 2026-05-02 114851" src="https://github.com/user-attachments/assets/1ff27560-02d0-47cf-bfd2-2e954e3bd978" />

Seems like one of item that is secretly hidden
<img width="734" height="556" alt="Screenshot 2026-05-02 115050" src="https://github.com/user-attachments/assets/9ce43721-5ed6-451b-a11e-e6aa4ba1f332" />

Do `hexedit` to findout more about it
<img width="764" height="514" alt="Screenshot 2026-05-02 115508" src="https://github.com/user-attachments/assets/20fba0a7-439f-4671-89fb-1d8a6952de08" />
This one is the secret photo. Change it from '.png' to '.PNG'
<img width="768" height="543" alt="Screenshot 2026-05-02 115521" src="https://github.com/user-attachments/assets/249f02a0-3649-43d2-8e07-db0558b59baf" />

The Image reveal
<img width="934" height="319" alt="Screenshot 2026-05-02 120816" src="https://github.com/user-attachments/assets/fb85c5f5-4bc7-4e28-b0b4-99747d9946ab" />

Now we try to find about hidden file inside a photo by using `steghide` 
`steghide --extract -sf`
<img width="725" height="393" alt="Screenshot 2026-05-02 120808" src="https://github.com/user-attachments/assets/52bddd7a-e632-4420-8ffb-3b21cf502798" />

 
 Enter 'password' for passphrase then 'Unzip' the file and read it by open/using `cat` command
<img width="607" height="376" alt="Screenshot 2026-05-02 120946" src="https://github.com/user-attachments/assets/abf84c71-a95a-4089-bb8b-6ceeca02927e" />

Found the `M3tahuman` is something can be use.

Now do ssh slade@10.48.144.254 and do sudo by using `M3tahuman` as a password
<img width="698" height="362" alt="Screenshot 2026-05-02 121146" src="https://github.com/user-attachments/assets/a6904573-9110-4cb9-b1ca-0254b6af96a1" />

Do `ls -a` to see all directory and use `cat` to see what inside
Found Flag 1
<img width="778" height="336" alt="Screenshot 2026-05-02 121308" src="https://github.com/user-attachments/assets/9cb305b2-c633-4cd3-a1c0-3a749be9698e" />

Now, to access the root user, upon doing sudo -l, it reveals this
Why sudo -l , which shows what commands you’re allowed to run as another user (usually root) without needing full root access.
It Show /usr/bin/pkexec with permissions such as -rwsr-xr-x, indicating that the Set User ID (SUID) bit is enabled. This implies that pkexec runs with the rights of the file owner, root, rather than the current user, whenever any user runs it. As part of Polkit, the application pkexec enables users to run commands as another user, usually root, following appropriate authentication.

`sudo pkexec /bin/bash` then `ls -a` and view all file `cat`
<img width="768" height="467" alt="Screenshot 2026-05-02 122102" src="https://github.com/user-attachments/assets/28969a4f-3f24-47f6-b3ca-3de6e8a2f462" />
### Got the last flag ✅




