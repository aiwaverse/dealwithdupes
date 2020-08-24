# Deal With Dupes: A Python Script to Search and Remove Duplicate Images 

Deal With Dupes is a simple Python script made to "deal" with folders that contains large amount of image files and with duplicates spread across different sub folders, specially duplicates of different sizes.

## Installation

Simply clone the repository and use the python command to run it:

```bash
python dealwithdupes.py
```

## Usage
The idea behind this script is to have a single place to identify and delete duplicates of images, duplicates including similar images in this case. It accepts a priority folder list, which allows the user to specify which folders should keep the copy of the file, if any. It will try to decide on it's own the best file to keep, it will look to size, then format (png or jpg), then the priority list. If it's not enough, it will ask the user and give an option to view the images and choose one (or skip the decision, in the case of a false positive).

The program needs to generate a structure with each image hash, which can take some time depending on the algorithm and number of files. On my machine, whash took roughly 45 minutes on a folder with 23500 images.

The default behavior will send the duplicates that weren't chosen to the trash, this can be changed with the ```--delete``` flag.

This program supports a few command line options, they can be viewed using:
```bash
python dealwithdupes.py --help
```
The ```--folder``` option specifies the root folder to run the program. If omitted, it's assumed to be the current folder:
```bash
python dealwithdupes.py --folder /home/Mariya/Pictures/Holiday-Season
```
The ```--priority-list``` option specifies a list of folders that should be prioritized to have the copy of the file, it's used as a string, so there's no need for a full path, for example:
```bash
python dealwithdupes.py --folder /home/Mariya/Pictures/Holiday-Season --priority-list 2020 Extras
```
Will, in the case of a duplicate found both in the folder 2020 and Extras, delete the Extras one and keep the 2020. The first one has the highest priority and so on, any omitted folder is assumed to have the lowest possible priority.

Important to keep in mind that it doesn't matter where 2020 is on the path of the file, or any other folder specified there.

The ```--hash``` argument specifies with hashing algorithm to use for the Images, possible values are ```ahash```, ```phash```, ```dhash``` and ```whash```, ```whash``` being the default if none is specified. For a description of each, see the [ImageHash module](https://pypi.org/project/ImageHash/) on PyPi. For example:
```bash
python dealwithdupes.py --hash ahash
```
Will use the average hash algorithm, on the current folder, with no priority on folders.

On the last, the flags ```--non-recursive``` will make the program search only on the specified folder, no sub folders. And the ```--delete``` flag will permanently delete any duplicates found, instead of sending them to the trash, which is the default behaviour.

## License
[MIT](https://choosealicense.com/licenses/mit/)
