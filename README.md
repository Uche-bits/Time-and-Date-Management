# Time-and-Date-Management
#Create a class to handle time and date operations, with methods to:  - Add or subtract days, hours, minutes - Format dates in different styles (e.g., DD/MM/YYYY, MM/DD/YYYY) - Calculate time differences
#from datetime import datetime, timedelta

class DateTimeManager:
    

    def __init__(self, start_datetime=None):
        
        if start_datetime is None:
            self.current_datetime = datetime.now()
        else:
            if not isinstance(start_datetime, datetime):
                raise TypeError("start_datetime must be a datetime object.")
            self.current_datetime = start_datetime
    
    def add_time(self, days=0, hours=0, minutes=0):
        self.current_datetime += timedelta(days=days, hours=hours, minutes=minutes)
    
    def subtract_time(self, days=0, hours=0, minutes=0):
        self.current_datetime -= timedelta(days=days, hours=hours, minutes=minutes)

    def format_date(self, style="MM/DD/YYYY"):
        
        format_map = {
            "DD/MM/YYYY": "%d/%m/%Y",
            "MM/DD/YYYY": "%m/%d/%Y",
            
            "Full": "%A, %B %d, %Y"
        }
        
        format_string = format_map.get(style, style)
        return self.current_datetime.strftime(format_string)

    def calculate_difference(self, other_datetime):
        if not isinstance(other_datetime, datetime):
            raise TypeError("other_datetime must be a datetime object.")
            
        return self.current_datetime - other_datetime

# Example Usage
if __name__ == "__main__":
    print("--- Initializing with Current Time ---")
    current_time_manager = DateTimeManager()
    print(f"Current Time: {current_time_manager.current_datetime}")
    print(f"Formatted (MM/DD/YYYY): {current_time_manager.format_date('MM/DD/YYYY')}")
    print(f"Formatted (Full): {current_time_manager.format_date('Full')}")

    # Add time

    print("\n--- Adding Time ---")
    current_time_manager.add_time(days=10, hours=4, minutes=30)
    print(f"After adding 10 days, 4 hours, and 30 minutes: {current_time_manager.current_datetime}")
    print(f"Formatted: {current_time_manager.format_date('Full')}")

    # Subtract time

    print("\n--- Subtracting Time ---")
    current_time_manager.subtract_time(hours=4, minutes=30)
    print(f"After subtracting 4 hours and 30 minutes: {current_time_manager.current_datetime}")

    # 4. Calculate time difference

    print("\n--- Calculating Time Difference ---")
    # Let's create another datetime object to compare against
    future_date_manager = DateTimeManager(datetime(2026, 1, 1, 10, 0, 0))
    print(f"Future Date: {future_date_manager.current_datetime}")

    # The difference will be from the future date to our current modified date

    time_difference = future_date_manager.calculate_difference(current_time_manager.current_datetime)
    print(f"Time difference is: {time_difference}")
    print(f"This is equal to: {time_difference.days} days and {time_difference.seconds // 3600} hours.")
