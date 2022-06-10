# sharedWhiteboard
This is Assignment 2 of Distributed System.

## 1 Problem Context
In this project, a shared whiteboard allows multiple users to draw simultaneously on a canvas. They can draw lines and shapes such as circles, squares and texts with 16 different colors and a changeable line width. Additionally, users can communicate with each other by typing text messages in the chat box. All the online users can see their peers at the same time. The first user to create the whiteboard will become the manager, who has the rights to kick out any person and new, save, close a whiteboard at any time.

## 2 System Architecture
![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/archi.png)

A client-server architecture is implemented for this whiteboard project. The user information and painting information are stored on the central server. The server and client communicate by RMI. When the information is updated, they can call and recall each other to keep the consistency quickly.

Here are the reasons why I choose this client-server architecture:
1. Less time on updating and syncing data. Since there is only one server.
2. Easy to maintain the security.
3. Convenient for a client to connect and disconnect.
4. Less cost for such a small system with certain users.

## 3 Communication Protocols
In this project, Java RMI is chosen to implement all the communication. The transport protocol is JRMP (Java Remote Method Protocol). It is a convenient protocol that support Java only and it can bind and call remote objects.
Two remote objects are identified in this project: iClient and iWhiteBoard.

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/remoteuml.png)

When a user tries to create or join a whiteboard, first the iClient remote object will be created for a registered online user. And when they start to draw, chat and other whiteboard-related operations, the iWhiteBoard remote object will be called.
We have two classes to implement the iClient interface: CreateWhiteBoard and JoinWhiteBoard, representing the manager and user sides. The iWhiteBoard interface is implemented in server side.

## 4 Design Diagrams
Manager and user:

simpleBoard is the GUI for all the users. We classify the role by a boolean param and the menu(File and kickout) function will be displayed only for manager.

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/uml2.png)

RMIServer and other Listeners for whiteboard:

The picListener and JsliderListener are both for manager and users; Only itemListerner is for manager to handle the menu function(File, kick out).

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/uml3.png)

## 5 User Interface
The GUI for manager:

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/mnggui.png)

The server will ask manager for permission by a window:

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/mngmsg.png)

The GUI for client:

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/cgui.png)

Sending message in chat box:

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/chat.png)

Draw different shapes:

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/paint.png)

Kick out user:

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/kick.png)

File menu:

![image](https://github.com/yanyy5/sharedWhiteboard/blob/main/pics/file.png)

## 6 Run the .jar file
To start the RMI registry:
```
java -jar server.jar <port-number>
```
To start the manager:
```
java -jar CreateWhiteBoard.jar <server-address> <port-number> <username>
```
To start the client:
```
java -jar JoinWhiteBoard.jar <server-address> <port-number> <username>
```
