# VNC

To get the vnc server on mac working use https://github.com/stweil/OSXvnc

and for the client side use this alias

alias macvnc="ssh -NfL 5900:localhost:5900 jeff@_____ && vncviewer localhost:5900"
