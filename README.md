class HotelReservationSystem:
    def __init__(self):
        self.rooms = {}  # Stores room details
        self.bookings = []  # Stores bookings

    def add_room(self, room_number, room_type, price):
        if room_number not in self.rooms:
            self.rooms[room_number] = {"type": room_type, "price": price, "available": True}
            print(f"Room {room_number} added successfully!")
        else:
            print("Room already exists.")

    def view_available_rooms(self):
        print("\nAvailable Rooms:")
        for room, details in self.rooms.items():
            if details["available"]:
                print(f"Room {room} - Type: {details['type']}, Price: ${details['price']}")
        print()

    def book_room(self, room_number, customer_name):
        if room_number in self.rooms and self.rooms[room_number]["available"]:
            self.rooms[room_number]["available"] = False
            self.bookings.append({"room": room_number, "customer": customer_name})
            print(f"Room {room_number} booked successfully for {customer_name}.")
        else:
            print("Room is not available or doesn't exist.")

    def cancel_booking(self, room_number):
        for booking in self.bookings:
            if booking["room"] == room_number:
                self.bookings.remove(booking)
                self.rooms[room_number]["available"] = True
                print(f"Booking for room {room_number} has been canceled.")
                return
        print("No booking found for this room.")

    def view_bookings(self):
        print("\nCurrent Bookings:")
        if not self.bookings:
            print("No bookings available.")
        for booking in self.bookings:
            print(f"Room {booking['room']} - Customer: {booking['customer']}")
        print()


# Main Program
def main():
    system = HotelReservationSystem()
    while True:
        print("\nHotel Reservation System")
        print("1. Add Room")
        print("2. View Available Rooms")
        print("3. Book Room")
        print("4. Cancel Booking")
        print("5. View Bookings")
        print("6. Exit")

        choice = input("Enter your choice: ")
        if choice == "1":
            room_number = input("Enter room number: ")
            room_type = input("Enter room type (Single/Double/Suite): ")
            price = float(input("Enter price per night: "))
            system.add_room(room_number, room_type, price)
        elif choice == "2":
            system.view_available_rooms()
        elif choice == "3":
            room_number = input("Enter room number to book: ")
            customer_name = input("Enter customer name: ")
            system.book_room(room_number, customer_name)
        elif choice == "4":
            room_number = input("Enter room number to cancel booking: ")
            system.cancel_booking(room_number)
        elif choice == "5":
            system.view_bookings()
        elif choice == "6":
            print("Exiting... Thank you!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()

