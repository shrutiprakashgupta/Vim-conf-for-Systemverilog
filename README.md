# Installing Neovim and Plugins for working with SystemVerilog

```sh
cd ~
apt-get install neovim
mkdir .config/nvim 
cd .config/nvim && nvim init.vim
#init.vim provided in the repo
```

## Using vim-plug for installing plugins

```sh
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
:PlugInstall
```

## Using coc.nvim for autocompletions, suggestions and linting

```sh
sudo apt-get install nodejs
sudo apt-get install npm
sudo npm install -g n
sudo n latest
sudo npm install -g @imc-trading/svlangserver
:CocConfig
```

Copy the following to the file opened here (coc-config.json) and update the paths </br>

```json
{
    "languageserver": {
        "svlangserver": {
            "module": "/INSTALLATION/PATH/lib/svlangserver.js",
            "filetypes": ["systemverilog"],
            "settings": {
                "systemverilog.includeIndexing": ["**/*.{sv,svh}"],
                "systemverilog.excludeIndexing": ["test/**/*.sv*"],
                "systemverilog.defines" : [],
                "systemverilog.launchConfiguration": "/TOOL/PATH/verilator -sv -Wall --lint-only",
                "systemverilog.formatCommand": "/TOOL/PATH/verible-verilog-format"
            }
        }
    }
}
```

```sh
#search for the path to svlangserver/main.js 
#Using Verilator and Verible-verilog-format for linting and syntax checking
sudo apt-get install verilator
#download latest released binary from https://github.com/chipsalliance/verible
tar -xvz verible-v0.0-1789-g43d1b6fe-CentOS-7.9.2009-Core-x86_64.tar.gz
sudo cp verible-v0.0-1789-g43d1b6fe/bin/* /bin/
sudo mkdir /usr/share/verible/
sudo cp verible-v0.0-1789-g43d1b6fe/share/verible/* /usr/share/verible/
sudo mkdir /usr/share/man/verible/
sudo cp verible-v0.0-1789-g43d1b6fe/share/man/man1/* /usr/share/man/verible/
#Update paths to main.js, verilator and verible-verilog-format in the config file opened above
```
