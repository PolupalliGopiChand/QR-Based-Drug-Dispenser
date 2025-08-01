import RPi.GPIO as GPIO
import time
import cv2
from pyzbar.pyzbar import decode

# Motor Pin Configuration
MOTOR_PINS = {
    "Shiva": [17, 18, 27, 22],  # GPIO pins for Motor 1
    "Gopi": [5, 6, 13, 19],     # GPIO pins for Motor 2
    "Narsi": [12, 16, 20, 21],  # GPIO pins for Motor 3
}

# Setup GPIO pins
GPIO.setmode(GPIO.BCM)
for pins in MOTOR_PINS.values():
    for pin in pins:
        GPIO.setup(pin, GPIO.OUT)

# Step sequence for 28BYJ-48 in half-step mode
step_sequence = [
    [1, 0, 0, 0],
    [1, 1, 0, 0],
    [0, 1, 0, 0],
    [0, 1, 1, 0],
    [0, 0, 1, 0],
    [0, 0, 1, 1],
    [0, 0, 0, 1],
    [1, 0, 0, 1],
]

# Reverse step sequence for Narsi motor only
step_sequence_reverse = list(reversed(step_sequence))

# Function to set the motor pins
def set_pins(step, pins):
    for i in range(4):
        GPIO.output(pins[i], step[i])

# Rotate stepper motor
def rotate(pins, rotations=1, steps_per_rotation=512, delay=0.001, reverse=False):
    total_steps = rotations * steps_per_rotation
    sequence = step_sequence_reverse if reverse else step_sequence
    for _ in range(total_steps):
        for step in sequence:
            set_pins(step, pins)
            time.sleep(delay)

# QR Code Reader Function
def qr_reader():
    cap = cv2.VideoCapture(0)
    if not cap.isOpened():
        print("Error: Could not open webcam.")
        return

    print("QR Code Reader: Looking for QR codes...")
    while True:
        ret, frame = cap.read()
        if not ret:
            print("Error: Failed to capture frame.")
            break
        decoded_objects = decode(frame)
        if decoded_objects:
            for obj in decoded_objects:
                qr_data = obj.data.decode("utf-8")
                qr_type = obj.type
                print(f"Detected QR Code: Type: {qr_type}, Data: {qr_data}")
                entries = qr_data.split()
                for entry in entries:
                    entry = entry.strip()
                    if not entry:
                        continue
                    name = ''.join(filter(str.isalpha, entry))
                    num = ''.join(filter(str.isdigit, entry))
                    rotations = int(num) if num.isdigit() else 1
                    if name in MOTOR_PINS:
                        reverse = name == "Narsi"  # Only reverse for Narsi motor
                        print(f"Activating motor '{name}' with {rotations} rotations ({'reversed' if reverse else 'normal'} direction)...")
                        rotate(MOTOR_PINS[name], rotations=rotations, reverse=reverse)
                    else:
                        print(f"No motor configuration found for '{name}'")
                cap.release()
                cv2.destroyAllWindows()
                return
        cv2.imshow("QR Code Reader", frame)
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break

    cap.release()
    cv2.destroyAllWindows()

try:
    qr_reader()
finally:
    GPIO.cleanup()
