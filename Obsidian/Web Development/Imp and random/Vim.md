search across codebase --- leader+sg

:%s/tobeReplaced/replace/g --- find and replace 
:%s/find/replace/g
/find --- finds the object
/find + enter + n ---- find and reach /// n gets u to the next instance 

### LSP
leader + gd --- go to defination 
K --- like in Vs we [ hover over  to see defination,types ]

get comfortable with [ leader + c ]

leader + cr --- smart replace // this also replace the refference values
leader + cf -- format

code action --- leader + ca
remove unsed imports --- leader + cR
organize imports --- leader + co

------------------------
---------------------------------------
### in VS code 
serach files- -- ctrl + t
ctrl+shift+ f --- search though the codebase
ctrl+shift+ h --- find, replace 

--------------------
--------------------

:q!  -> exit forcefully, doesnt save 
:q --> exiting without saving
:wq! -> save and exit 
:w --> only saves , doesnt exit

vi a.txt -> creates an empty file(a.txt) and opens it in vim. but u need to save it to create it 

:Explore
% --- add a file
d -- add a directory

### splitting windows
split horizontally -- leader -
split verdtically -- leader |
navigate windows -- ctrl +[h/j/k/l]
switching buffers --   ///buffers are the coding tabs 
[b -- go to left
]b -- go to right 

### navigation
gg -- top of the file 
G -- bottom of the file 
0 -- start of the line 
$ -- end of the line 
e --- Fast forward 
//vim uses relative line no
linenumber (j/k) ---- to jump to that exact line no.

open terminal --- leader + ft 

rename -- r
delete file -- d

dd --- cut  a line in the code

u --- undo in vim
r --- redo 
d --- delete
p --- paste
v --- select 
d --- delete
y---- copy

vi --- select inside 
vi( ---- select inside ()
vi" --- select inside " "
similarly 
di( -- delete everything inside ()




