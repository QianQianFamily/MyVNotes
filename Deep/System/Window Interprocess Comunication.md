# Interprocess Comunication(IPC)

[IPC 9 Methods](https://docs.microsoft.com/en-us/windows/desktop/ipc/interprocess-communications)

## Clipboard
All applications should support the clipboard for those data formats that they understand. For example, a text editor or word processor should at least be able to produce and accept clipboard data in pure text format. For more information, see Clipboard.

## COM
OLE supports compound documents and enables an application to include embedded or linked data that, when chosen, automatically starts another application for data editing. This enables the application to be extended by any other application that uses OLE. COM objects provide access to an object's data through one or more sets of related functions, known as interfaces. For more information, see COM and ActiveX Object Services.

## Data Copy
Data copy can be used to quickly send information to another application using Windows messaging. For more information, see Data Copy.

## DDE
DDE is not as efficient as newer technologies. However, you can still use DDE if other IPC mechanisms are not suitable or if you must interface with an existing application that only supports DDE. For more information, see Dynamic Data Exchange and Dynamic Data Exchange Management Library.
 
## File Mapping
File mapping is an efficient way for two or more processes on the same computer to share data, but you must provide synchronization between the processes. For more information, see File Mapping and Synchronization.

## Mailslots
Mailslots offer an easy way for applications to send and receive short messages. They also provide the ability to broadcast messages across all computers in a network domain. For more information, see Mailslots.

## Pipes
Anonymous pipes provide an efficient way to redirect standard input or output to child processes on the same computer. Named pipes provide a simple programming interface for transferring data between two processes, whether they reside on the same computer or over a network. For more information, see Pipes.

## RPC
RPC is a function-level interface, with support for automatic data conversion and for communications with other operating systems. Using RPC, you can create high-performance, tightly coupled distributed applications. For more information, see Microsoft RPC Components.

## Windows Sockets
Windows Sockets is a protocol-independent interface capable of supporting current and emerging networking capabilities. For more information, see Windows Sockets 2.