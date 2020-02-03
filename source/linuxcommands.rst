Linux commands
==============

A table with common Linux commands:

+----------------------------------+----------------------------------+
| **Command**                      | **Explanation**                  |
+==================================+==================================+
| cd                               | Change directory                 |
+----------------------------------+----------------------------------+
| cd ~                             | Change directory to home         |
+----------------------------------+----------------------------------+
| cd ..                            | Go back one folder               |
+----------------------------------+----------------------------------+
| cd ../..                         | Go back two folders              |
+----------------------------------+----------------------------------+
| pwd                              | Show current folder location     |
+----------------------------------+----------------------------------+
| ls                               | See files and folders in your    |
|                                  | current location                 |
+----------------------------------+----------------------------------+
| cd <*directory*>                 | CD into <*directory*>            |
+----------------------------------+----------------------------------+
| sudo <*command*>                 | sudo stands for: “Super User     |
|                                  | DO”. Give administrator rights   |
|                                  | to the <*command*>               |
+----------------------------------+----------------------------------+
| sudo shutdown now                | Shuts down the computer          |
+----------------------------------+----------------------------------+
| sudo reboot                      | Restarts the computer            |
+----------------------------------+----------------------------------+
| echo "hello"                     | Prints “hello” to the terminal   |
+----------------------------------+----------------------------------+
| <*command1*> :math:`|`           | The :math:`|` makes the output   |
| <*command2*>                     | of <*command1*> to be sent to    |
|                                  | <*command2*>                     |
+----------------------------------+----------------------------------+
| grep <*text*> <*file*>           | Finds and displays lines which   |
|                                  | contains <*text*> in the         |
|                                  | <*file*>                         |
+----------------------------------+----------------------------------+
| echo "Test 1 2 3" :math:`|` grep | Prints "Test 1 2 3" into the     |
| 2                                | next command due to :math:`|`.   |
|                                  | This text is input into the grep |
|                                  | command. Grep searches for "2"   |
|                                  | and shows where it found it. The |
|                                  | :math:`|` may not be copied      |
|                                  | correctly to the terminal        |
+----------------------------------+----------------------------------+
| rm <*file*>                      | Deletes <*file*>                 |
+----------------------------------+----------------------------------+
| rm -r <*folder*>                 | Deletes <*folder*> and           |
|                                  | everything inside it             |
+----------------------------------+----------------------------------+
| mkdir <*folder*>                 | Makes a <*folder*>               |
+----------------------------------+----------------------------------+
| chmod <*file*>                   | Changes mode of a <*file*>       |
+----------------------------------+----------------------------------+
| chmod +x <*file*>                | Lets <*file*> be executable. +   |
|                                  | means to add. +x means add       |
|                                  | execution (x).                   |
+----------------------------------+----------------------------------+
| ./<*file*>                       | Executes <*file*> if <*file*> is |
|                                  | in the current directory         |
+----------------------------------+----------------------------------+
| <*folder*>/<*file*>              | Executes <*file*> that is        |
|                                  | located in <*folder*>            |
+----------------------------------+----------------------------------+
| ssh -X <*username*>@<*hostname*> | Opens a secure shell (SSH) for   |
|                                  | user <*username*> on computer    |
|                                  | <*hostname*>. The -X lets        |
|                                  | display commands be sent through |
|                                  | SSH                              |
+----------------------------------+----------------------------------+
| ssh -X jetbot@192.168.0.3        | Opens ssh to jetbot              |
+----------------------------------+----------------------------------+
| python <*file.py*>               | Run Python version 2 with input  |
|                                  | file <*file.py*>                 |
+----------------------------------+----------------------------------+
| python3 <*file.py*>              | Run Python version 3 with input  |
|                                  | file <*file.py*>                 |
+----------------------------------+----------------------------------+

Tmux commands
-------------

| Assumes that .tmux.conf is downloaded from canvas and put into
  /home/jetbot

+----------------+----------------------------------------------------+
| **Command**    | **Explanation**                                    |
+----------------+----------------------------------------------------+
| CTRL a         | Enter command mode. Every other command in this    |
|                | list starting with *cm* requires you to be in      |
|                | command mode. You need to re-enter command mode    |
|                | for each command                                   |
+----------------+----------------------------------------------------+
| *cm* -         | Split display horizontally                         |
+----------------+----------------------------------------------------+
| *cm* :math:`|` | Split display vertically                           |
+----------------+----------------------------------------------------+
| tmux detach    | Go out of the tmux session and keep it running in  |
|                | the background                                     |
+----------------+----------------------------------------------------+
| tmux attach    | Go back into the tmux session that is already      |
|                | running                                            |
+----------------+----------------------------------------------------+
