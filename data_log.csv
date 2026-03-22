from opcua import Client
import pandas as pd
import time
from datetime import datetime

OPC_URL = "opc.tcp://192.168.0.2:4840"
NODE_ID = "ns=4;i=2"

client = Client(OPC_URL)

try:
    print("Connecting to PLC...")
    client.connect()
    print("Connected!")

    node = client.get_node(NODE_ID)

    while True:
        value = node.get_value()
        timestamp = datetime.now()

        print(f"Value: {value} | Time: {timestamp}")

        df = pd.DataFrame([[timestamp, value]], columns=["Time", "Value"])
        df.to_csv("data_log.csv", mode='a', header=False, index=False)

        time.sleep(2)

except Exception as e:
    print("Error:", e)

finally:
    client.disconnect()
    print("Disconnected")
