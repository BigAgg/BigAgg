- 👋 Hi, I’m @BigAgg
- 👀 I’m interested in coding and gaming
- 🌱 I’m currently learning python and c++
- 💞️ I’m looking to collaborate on nothing in particular atm
- 📫 How to reach me: bigagg@jahraus-online.de

I am looking forward to code an open source python erp program using PySimpleGUI called 'simplERP'.
I also wish to create a rogue-like game using pygame with up to 4 players multiplayer.

<!---
BigAgg/BigAgg is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
___________________________________________________________________________________________________________________
server:

import socket
import threading
import time

HOST = "10.1.4.86"
PORT = 5050
FORMAT = "utf-8"
MAXPLAYERS = 4


def connection(conn, addr):
    try:
        with conn:
            if len(threading.enumerate()) - 1 > MAXPLAYERS:
                conn.sendall("The Server is full".encode(FORMAT))
                return
            print(f"[NEW CONNECTION] Connected to {addr}")
            conn.sendall("Connected".encode(FORMAT))
            data = None
            while data != "!DISCONNECT":
                data = conn.recv(1024).decode(FORMAT)
                if not data:
                    break
                print(data)
                if data == "!DISCONNECT":
                    break
                conn.sendall(data.encode(FORMAT))
            conn.sendall("Disconnected".encode(FORMAT))
            print(f"Disconnected {addr}")
    except ConnectionResetError:
        print(f"{addr} lost connection")


def main():
    print("[STARTING] Server is starting...")
    while 1:
        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
            s.bind((HOST, PORT))
            if len(threading.enumerate()) - 1 <= MAXPLAYERS:
                s.listen()
                print("[LISTENING] Server is listening...")
                conn, addr = s.accept()
                client = threading.Thread(target=connection, args=(conn, addr,))
                client.start()
                for thread in threading.enumerate():
                    print(thread.name)
            else:
                print("[SERVER MSG] Server is full")
                while len(threading.enumerate()) - 1 >= MAXPLAYERS:
                    time.sleep(2)


if __name__ == "__main__":
    main()
__________________________________________________________________________________________________________________________

client:

import socket
from time import perf_counter

HOST = "10.1.4.86"
PORT = 5050
FORMAT = "utf-8"

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    data = s.recv(1024).decode(FORMAT)
    if data == "Connected" and data != "The Server is full":
        print(data)
        while (inp := input()) != "!DISCONNECT":
            s.sendall(inp.encode(FORMAT))
            start_time = perf_counter()
            data = s.recv(1024).decode(FORMAT)
            print(f"Recieved message in {perf_counter() - start_time}")
            print(data)
        s.sendall(inp.encode(FORMAT))
        data = s.recv(1024).decode(FORMAT)
        print(data)
    else:
        print(data)
    s.close()

--->
