# UP HTTP Server

*Really* simple wrapper around Flask / Waitress, dropping in as a replacement for the classic "python3 -m http.server". Useful for security testing ¯\\_(ツ)_/¯

This tool has a couple of advantages over the simple version:
* Optionally show request headers -- useful for debugging or if you're looking for connections back from a target webserver
* Pretty colours to differentiate requests (can be disabled with `--accessible` or `-c`/`--no-colour`)
* Disable file-sharing (this increases security if you're only wanting connection info -- will respond with 404 to every request)
* Display information about the working environment (e.g. network addresses, current directory, files being served, etc) at start and whenever you press enter

Help Menu:
```
usage: up [-h] [-v] [-q] [-p PORT] [-i IP] [-d DIRECTORY | --no-serve]
          [--accessible | -c] [-dc]

UP Simple HTTP server for debugging / hacking

options:
  -h, --help            show this help message and exit
  -v, --verbose         Show request headers / information (you probably want
                        this active)
  -q, --quiet           Don't show information on startup
  -p PORT, --port PORT  The port to serve on. Defaults to port 80
  -i IP, --ip IP        The IP to serve on. Defaults to all interfaces
                        (0.0.0.0)
  -d DIRECTORY, --directory DIRECTORY
                        Directory to serve files from. Defaults to current
                        working directory
  --no-serve            Do not serve files
  --accessible          Disable ASCII art (automatically adds --no-colour)
  -c, --no-colour       Disable colour printing
  -dc, --disable-cors   Add headers to disable CORS
```

## Installation Instructions

### Venv Installation

Literally just a Python script. Do something like this to install dependencies and add the script to your PATH:
```bash
git clone https://github.com/MuirlandOracle/up-http-tool up && cd up
python3 -m venv env
./env/bin/python -m pip install -r requirements.txt
cat << EOF | sudo tee /usr/local/bin/up 2>&1 &>/dev/null
#!/usr/bin/env sh
$(pwd)/env/bin/python $(pwd)/up \$@
EOF
sudo chmod 555 /usr/local/bin/up
```

### Simple Installation (not good practice, but if you like living on the edge... do this)
```bash
git clone https://github.com/MuirlandOracle/up-http-tool
cd up-http-tool
pip install -r requirements.txt
cp up /usr/bin
./up
```

Note, this has been tested on Kali Linux... and that is it. I developed this to make life easier when testing webapps / applications that might callback over HTTP -- you are more than welcome to make use of it yourself, but please don't expect full product support!
