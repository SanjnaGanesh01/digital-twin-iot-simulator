import csv

EXPECTED_TEMP = 25
EXPECTED_HUMID = 60

print("Digital Twin Simulator Started\n")

with open("sensor_data.csv", "r") as file:
    reader = csv.DictReader(file)

    for i, row in enumerate(reader, start=1):
        temp = float(row["temperature"])
        humid = float(row["humidity"])

        temp_diff = abs(temp - EXPECTED_TEMP)
        humid_diff = abs(humid - EXPECTED_HUMID)

        anomaly_score = temp_diff + humid_diff

        print(f"Reading {i}")
        print(f"Temperature: {temp}°C | Humidity: {humid}%")

        if anomaly_score <= 5:
            status = "HEALTHY"
        elif anomaly_score <= 10:
            status = "WARNING"
        else:
            status = "CRITICAL"

        print(f"Status: {status}\n")
