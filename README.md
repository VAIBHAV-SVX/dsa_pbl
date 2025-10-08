import random
from collections import deque

class Node:
    def __init__(self, humidity, temperature, rainfall):
        self.humidity = humidity
        self.temperature = temperature
        self.rainfall = rainfall
        self.next = None

class WeatherDataLinkedList:
    def __init__(self):
        self.head = None

    def insert(self, humidity, temperature, rainfall):
        new_node = Node(humidity, temperature, rainfall)
        if not self.head:
            self.head = new_node
        else:
            temp = self.head
            while temp.next:
                temp = temp.next
            temp.next = new_node

    def display(self):
        temp = self.head
        print("\n📊 Weather Data (Linked List):")
        while temp:
            print(f"Humidity: {temp.humidity}%, Temperature: {temp.temperature}°C, Rainfall: {temp.rainfall}mm")
            temp = temp.next


class Stack:
    def __init__(self):
        self.stack = []

    def push(self, prediction):
        self.stack.append(prediction)

    def display(self):
        print("\n📚 Prediction History (Stack):")
        for i, pred in enumerate(reversed(self.stack), 1):
            print(f"{i}. {pred}")


class LocationQueue:
    def __init__(self):
        self.queue = deque()

    def enqueue(self, location):
        self.queue.append(location)

    def dequeue(self):
        if self.queue:
            return self.queue.popleft()
        else:
            return None


def predict_cloud_burst(humidity, temperature, rainfall):
    """
    Simple rule-based logic:
    - High humidity (>80%)
    - Moderate/low temperature (<25°C)
    - High rainfall (>100mm)
    """
    if humidity > 80 and temperature < 25 and rainfall > 100:
        return "⚠️ Cloud Burst Risk Detected!"
    else:
        return "✅ No Cloud Burst Risk."


# ---------- Main Function ----------
def main():
    print("🌧️ Cloud Burst Prediction System 🌧️")
    print("Type 'exit' anytime to stop.\n")

    location_queue = LocationQueue()
    weather_list = WeatherDataLinkedList()
    prediction_stack = Stack()

    while True:
        location = input("\nEnter the location: ").strip()
        if location.lower() == "exit":
            print("\n👋 Exiting Cloud Burst Prediction System...")
            break

        location_queue.enqueue(location.title())

        humidity = random.randint(50, 100)
        temperature = random.randint(10, 40)
        rainfall = random.randint(0, 200)

        weather_list.insert(humidity, temperature, rainfall)

        prediction = predict_cloud_burst(humidity, temperature, rainfall)
        prediction_stack.push(f"{location.title()}: {prediction}")

        print(f"\n📍 Location: {location.title()}")
        print(f"Humidity: {humidity}%")
        print(f"Temperature: {temperature}°C")
        print(f"Rainfall: {rainfall}mm")
        print(f"\n🔍 Prediction Result: {prediction}")

        weather_list.display()
        prediction_stack.display()

if __name__ == "__main__":
    main()
