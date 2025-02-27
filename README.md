# UDP-and-TCP-client-communication
This project implements a messaging server with UDP and TCP client communication, handling subscriptions and message broadcasting:


    Message Packet Structure: The packet contains three main fields for message transmission from UDP clients, with an extended type field to support commands such as subscribe or exit.
    Additionally, two extra fields are included to transmit the UDP client's address.

    Server Implementation (server.cpp): The server acts as an intermediary between clients. It initializes both UDP and TCP sockets to receive messages.
    Using the run_chat_multiserver function, it creates a poll to multiplex between the UDP socket, TCP socket, and standard input. When a TCP client requests a connection, 
    the server accepts it, receives the client's ID, and checks if the ID is already in use. If it is, the connection is rejected. Otherwise, the client can subscribe to topics,
    which are stored in a map where the key is the topic name and the value is a list of subscribed client IDs. When a message arrives via the UDP socket, the server checks the map
    for subscribers and forwards the message to any connected clients.

    Subscriber Implementation (subscriber.cpp): The subscriber is a TCP client that sends subscription or unsubscription commands and receives messages from the server.
    It establishes a TCP connection, sends its ID to the server, and then subscribes or unsubscribes from topics as needed.
    When the subscriber receives a message, it either processes a disconnect command from the server or decodes a message from one of its subscribed topics.

This system allows for efficient message routing and subscription management between UDP clients and TCP subscribers.
