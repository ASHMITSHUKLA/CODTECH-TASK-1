# Port Scanner Program.
import socket

def port_scan(target, start_port, end_port):
    """
    Scan for open ports on a target system.

    Args:
        target (str): The IP address or hostname of the target system.
        start_port (int): The starting port number to scan.
        end_port (int): The ending port number to scan.

    Returns:
        A list of open ports.
    """
    open_ports = []
    for port in range(start_port, end_port + 1):
        try:
            # Create a socket object
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            # Set a timeout to avoid waiting indefinitely
            sock.settimeout(1)
            # Attempt to connect to the target port
            result = sock.connect_ex((target, port))
            if result == 0:
                # If the connection is successful, the port is open
                open_ports.append(port)
            sock.close()
        except socket.error as e:
            print(f"Error scanning port {port}: {e}")
    return open_ports

def main():
    target = input("Enter the IP address or hostname of the target system: ")
    start_port = int(input("Enter the starting port number to scan: "))
    end_port = int(input("Enter the ending port number to scan: "))

    open_ports = port_scan(target, start_port, end_port)

    if open_ports:
        print(f"Open ports on {target}: {open_ports}")
    else:
        print(f"No open ports found on {target} between {start_port} and {end_port}.")

if __name__ == "__main__":
    main()
