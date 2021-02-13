===================
Getting Started
===================

Hi (:

Neutron Unity Networking is a Unity package for multiplayer games.
Flexible matchmaking gets your players into rooms, channels and groups where objects can be synced over the network.

**Communication Types:**

:RPC: | ``Remote Procedure Calls are exactly what the name implies: method-calls on remote clients in the same local by broadcast.``
      | ``To enable remote calling for some method, you must apply the attribute.[RPC]``
      | ``RPC are sent from the client to the server.``

:APC: | ``One feature that sets Neutron aside from other Network packages is the support for "Authoritative Procedure Calls" (APCs).``
      | ``Is basically the same as RPC, except that: APC are sent from the server to the client.``

:RCC: | ``One feature that sets Neutron aside from other Network packages is the support for "Remote Creation Calls" (RCCs).``
      | ``These calls are global server events for clients, mainly used for the creation of the player.``

:ACC: | ``One feature that sets Neutron aside from other Network packages is the support for "Authoritative Creation Calls" (ACCs).``
      | ``Is basically the same as RCC, except that: ACC are sent from the server to the client.``

Neutron was created with the aim of serving all games,
from FPS to MMORPG and even simpler games, whatever you want.

Configuring the server
=========================

- Download package from the GitHub repository.
- Put in the Unity assets folder.

.. note:: Now let's create two layers necessary for the server to work, create the layer "ServerObject" and "ClientObject"

Now that we’ve finished the basics, let’s get started.

- Create an object like the one in the image.

.. image:: ..\\Images\\ServerController.png
   :class: img

- Create the Object "Server Controller".

.. note:: The name of the object doesn't matter

- Put the script "Neutron Server" in the object was created.
- The server is ready.

**Parameters:**

:Time Delta: | ``The completion time in seconds since the last frame.``
             | ``This property provides the time between the current and previous frame.``

:Channels: | ``Add server channels here.``
           | ``Internal ID: The value of this field must be unique.``
           | ``Name: The Channel Name.``
           | ``Count(ReadOnly): The number of players in this channel.``
           | ``Max Players: The maximum number of players on this channel.``

:Buffers: | ``Coming soon....``

:Rooms: | ``Rooms automatically created by the server.``
           | ``The rooms can also be created by the clients, except the channels.``

.. image:: ..\\Images\\ServerConfig.png
   :class: img

:Compression Mode: ``The type of data compression that will be used, the default is DEFLATE.``

:Server Port: ``The port on which the server listens for data.``

:Voice Port: ``The port on which the voice server listens for voice data.``

:BackLog: ``The maximum length of the pending connections queue``

:FPS: ``Frame rate of Server.``

:DPF: ``Amount of queue data processed per frame.``

:Send Rate: ``Delay between sending each packet, 0 will overload the CPU.``

:Quick Packets: ``Enables fast processing of TCP packets, note: if enabled, packets sent too often may fail.``

:No Delay: ``Gets or sets a value that disables a delay when send or receive buffers are not full.``

:Anti-Cheat: ``Activate or deactivate the server's anti-cheat.``

.. note:: AntiCheat leave it disabled if you use authority.

:Teleport Tolerance: ``Maximum teleport distance to detect the player.``

:SpeedHack Tolerance: ``Frequency with which packets arrive at the server per second.``

:URI Login: | ``Activate your local network, ex: ”Xampp“, and inside the``
            | ``"htdocs" folder create the Network folder and put the "login.php" script.``
            | ``A login script as example and find on GitHub.``

:Time Delta: ``The "time.DeltaTime" of server, is ReadOnly.``

:Channels: ``The server's pre-existing channels.``

.. note:: Ignore the tolerance if you do not use Anti-Cheat enabled, if you use authority, ignore this too. More if you use RPC to synchronize movements, do not ignore this.

.. note:: | Speed Tolerance: The calculation is: **n * 1000 = result; -> 1000 / result = final result;**
          | **eg: 0.1 * 1000 = 100 -> 1000/100 = 10;**
          | In other words, if you synchronize the movement via RPC every 0.1 second or 100 milliseconds, your speedhack tolerance will be 10.

Configuring the client
=========================

- Create de object "ClientController"

.. note:: The name of the object doesn't matter

- Create the connection script and put in object was created.
- put too "Neutron Physics Ignore".

.. image:: ..\\Images\\ClientController.png

- Ready :D

Configuring the connection
------------------------------

- First we need to create a Neutron instance.

.. code-block:: C#
   :linenos:

   void Start() {
      var clientInstance = Neutron.CreateClient(ClientType.MainPlayer); // this instance can be accessed by **Neutron.Client**
   }

.. tip:: The main instance (MainPlayer), "clientInstance" that you will see below can be accessed from other scripts through "Neutron.Client"

- Now let's record the events.

.. code-block:: C#
   :linenos:
   :emphasize-lines: 6

   void Start() {
      var clientInstance = Neutron.CreateClient(ClientType.MainPlayer); // this instance can be accessed by **Neutron.Client**

      //events

      clientInstance.onNeutronConnected += OnNeutronConnected; // registered method.
      clientInstance.Connect("localhost", 5055); // IP And Port to connect.
   }

- Registered method.

.. code-block:: C#
   :linenos:

   void OnNeutronConnected(bool success, Neutron localInstance) {
      Debug.Log("ready");
   }

- Ready, connection established.

Matchmaking
-------------

- Set the your nickname, First let's record the nickname change event.

.. note:: The nickname can be changed by both the client and the server. You can remove the client's permission to change the nickname on the server.

.. code-block:: C#
   :linenos:
   :emphasize-lines: 7

   void Start() {
      var clientInstance = Neutron.CreateClient(ClientType.MainPlayer); // this instance can be accessed by **Neutron.Client**

      //events

      clientInstance.onNeutronConnected += OnNeutronConnected; // registered method.
      clientInstance.onNicknameChanged += OnNickname; // nickname event.
      clientInstance.Connect("localhost", 5055); // IP And Port to connect.
   }

- Registered method.

.. code-block:: C#
   :linenos:

   void OnNickname(Neutron instance) {
      // Nickname has changed.
   }

**Create Room and Join Room/Channel:**

- We will record the events.

.. code-block:: C#
   :linenos:
   :emphasize-lines: 8, 9, 10

   void Start() {
      var clientInstance = Neutron.CreateClient(ClientType.MainPlayer); // this instance can be accessed by **Neutron.Client**

      //events

      clientInstance.onNeutronConnected += OnNeutronConnected; // registered method.
      clientInstance.onNicknameChanged += OnNickname; // nickname event.
      clientInstance.onPlayerJoinedChannel += OnJoinedChannel;
      clientInstance.onPlayerJoinedRoom += OnJoinedRoom;
      clientInstance.onCreatedRoom += OnCreatedRoom;
      clientInstance.Connect("localhost", 5055); // IP And Port to connect.
   }

- Registered methods.

.. code-block:: C#
   :linenos:

   void OnCreatedRoom(Room room, NeutronReader options, Neutron localInstance) {
      //Created
   }

   void OnJoinedRoom(Player player, int id, Neutron instance) {
      // Joined
   }

   void OnJoinedChannel(Player player, Neutron instance) {
      // Joined
   }

eg:

.. code-block:: C#
   :linenos:

   void OnNickname(Neutron instance) {
      instance.JoinChannel(0); // join to a channel 0. if a channel not exist in server, an error message will be displayed.
   }

- Creating a room

.. code-block:: C#

   public void CreateRoom() {
        Neutron.Client.CreateRoom("room name", 100, null, new NeutronWriter());

        // or instance.CreateRoom("room name", 100, null, new NeutronWriter());
   }