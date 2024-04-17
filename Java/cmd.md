# CMD relevant operation

> Some basic usages

1. using the form such as ```  d: ``` to change your disk directory in cmd.
2.  ```dir``` can investigate the content in current path, including directories, files and so forth.
3.  ```cd [full path]``` to get into a single directory.
4. ``` cd..``` can get back to the former directory.
5. ```cd \``` back to the disk directory.

* An interesting example

    How to open a .exe file only with cmd?

Intuitively, it can be simply to directly print ```cd [the file path]``` to get into the ```bin``` directory, and type the .exe file to lanch it.

However,  it's rather inconvinient cuz the operation of changing disk and a list of order are really repeated work. 

A simple method is add the bin path into environmental variable section in the computer. Then, once u open the cmd, just type the name and u can open it.

