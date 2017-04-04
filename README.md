# WebDAV
WebDAV implementation in InterSystems Caché

# Installation

1. Import code.
2. Create new `/` web application:
   - Dispatch Class: `WebDav.REST`
   - Allowed Authentication Methods: Unauthenticated
3. Execute in a terminal:
   - `Set ^WebDav.Settings("Folder") = path`, where `path` is directory - root of WebDAV server. Note that it must be without trailing slash.

   
# Linux file configuration

Set System call I/O table to UTF8. To do that, execute in a terminal:

```
%SYS>d ^NLS


1) Display current locale
2) Select defaults
3) Change locale
4) Display loaded settings
5) Advanced

NLS option? 2

1) Internal tables
2) I/O tables
3) CSP files
4) Date, time and number formats

Category of defaults? 2

Items marked with (*) represent the locale's original default

I/O table Current default
--------------------- --------------------

1) Process RAW (*)
2) Cache Terminal UTF8 (*)
3) Other terminal UTF8 (*)
4) File RAW (*)
5) Magtape RAW (*)
6) TCP/IP RAW (*)
7) System call RAW (*)
8) Printer RAW (*)

I/O table: 7

 1) RAW (*) 2) UTF8
 3) UnicodeLittle 4) UnicodeBig
 5) CP1250 6) CP1251
 7) CP1252 8) CP1253
 9) CP1255 10) CP437
11) CP850 12) CP852
13) CP866 14) CP874
15) EBCDIC 16) Latin2
17) Latin9 18) LatinC
19) LatinG 20) LatinH
21) LatinT

Selection for System call: 1 => 2

I/O table Current default
--------------------- --------------------

1) Process RAW (*)
2) Cache Terminal UTF8 (*)
3) Other terminal UTF8 (*)
4) File RAW (*)
5) Magtape RAW (*)
6) TCP/IP RAW (*)
7) System call UTF8
8) Printer RAW (*)

I/O table:

1 changed property. Save? Yes => <Saved>
```

# Linux firefox setup

We need to register `dav` protocol with firefox. To do that:

1. Type `about:config` into the Location Bar (address bar) and press Enter.
2. Right-click -> New -> Boolean -> Name: `network.protocol-handler.expose.dav` -> Value -> false
3. Next time you click a link of protocol-type foo you will be asked which application to open it with. Choose LibreOffice: `/usr/bin/loffice`

# Wireshark setup

1. For local development [install](https://wiki.wireshark.org/CaptureSetup/Loopback) Wireshark with loopback support.
2. Add capture filter: `port 57772`.
3. Start capture.
4. Add display filters:
   - http
   - http.user_agent contains "Microsoft"
   - http.request.method == "POST"
   - ip.dst == xxx.xxx.xxx.xxx && http