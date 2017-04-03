# WebDAV
WebDAV implementation in InterSystems Caché

# Installation

1. Import code.
2. Create new `/` web application:
   - Dispatch Class: `WebDav.REST`
   - Allowed Authentication Methods: Unauthenticated
3. Execute in a terminal:
   - `Set ^WebDav.Settings("Folder") = path`, where `path` is directory - root of WebDAV server. Note that it must be without trailing slash.
