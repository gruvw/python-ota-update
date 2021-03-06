# Python Over-The-Air Update

This is a little Python3 project which allows you to update a python program without needing to rerun it. You can take a look at the example folder of this repository in order to understand how this script works.

## Requirements

The only file you need in order to use this update system for python project is the _ota-update.py_. Keep in mind that in the directory where this script will be executed, files and folders will be created. I recommend executing this script inside an empty directory which will be used only for your python project.

It requires the [PrintBetter](https://github.com/gruvw/printbetter) python package in order to work.

## File architecture

The typical directory tree of a python project using the _ota-update.py_ script should look like this:

```text
.
├── deposit
├── logs
│   ├── logfile_DD-MM-YY_HH.MM.SS.log
│   └── ...
├── main
│   ├── main.py
│   └── ...
├── ota-update.py
```

* The _deposit_ folder is the place where you can put files from your python project. It can be assets, files or folders. The files inside the _main_ folder will be replaced by the new ones inside the _deposit_ folder once/if the _ota-update.py_ script is running. The file structure inside the deposit folder will be replicated inside the main folder. You should only place new files inside the deposit folder as opposed to placing your whole python project every time: nothing is automatically deleted from the main directory, files that are found inside the _deposit_ folder will be added to the _main_ folder or will replace the old ones.
* The _main_ folder is where your python project is. The _ota-update.py_ script will automatically execute the _main.py_ file inside it.
* The _logs_ folder is the place where you will find the logs generated by the [PrintBetter](https://github.com/gruvw/printbetter) python package used by the _ota-update.py_ script.

### Be careful

You need to run the _ota-update.py_ script directly from its parent directory!

For example:

```bash
cd users/gruvw/python-ota-update/example
python ota-update.py
```

### First execution

If there is no _deposit_ or _main_ folder in the same directory of the _ota-update.py_, the first execution of the script will create both of them (along with the _logs_ folder). It will then trow a "No _main.py_ inside the main directory." exception which is totally normal because the main directory has just been created so there is no _main.py_ file inside it yet. You can now place your python project files inside the freshly created _deposit_ folder and run the _ota-update.py_ script again. This will move your whole python project from the _deposit_ to the _main_ folder.

## How to use

Once you have your working python project inside the _main_ folder (see [First execution](#first-execution)), you may run the _ota-update.py_ script which will execute the _main.py_ inside the _main_ folder. You can now put new files and/or folders inside the _deposit_ folder while the script is running. The _main.py_ will automatically stop and the new files will be moved from the _deposit_ to the _main_ folder. The _main.py_ script will then start again automatically.

1. You should not put anything inside the _main_ folder by yourself, but rather put them inside the _deposit_ folder and run the _ota-update.py_
2. You can delete files from the _main_ folder if you need to, but you should not do so while the _ota-update.py_ is still running
3. You need to have a _main.py_ script inside the _main_ folder in order to use the _ota-update.py_ script properly
4. You can update any file that you want with the script, even the _main.py_ script. Just put it inside the _deposit_ folder
5. If you put some files inside the _deposit_ folder while the _ota-update.py_ script is not running, the files will be moved to the _main_ folder when you will run the script

## Why I created this

I created this file architecture/python script because I used to have to update a python script to a [Raspberry Pi](https://www.raspberrypi.org/) via FTP. I always needed to connect to the Raspberry Pi via VNC or SSH in order to:

1. Stop the currently running python script
2. Delete the old version of the python file
3. Run the new script that I just uploaded

Now, with this solution, I only need to run the _ota-update.py_ script once (or even auto-run at startup) and if I need to update my script or anything about my python project, I just transfer the files inside the _deposit_ folder via FTP. My script will start again automatically after the update.

## Issues / Pull requests

Fill free to open an issue if anything is not working for you. Pull requests are also welcome if you think about a feature, I would be happy to take a look at your code.
