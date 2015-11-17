import RPi.GPIO as GPIO
import time
GPIO.setmode(GPIO.BCM)
shutter_pin = 18
coil_A_1_pin = 4
coil_A_2_pin = 17
coil_B_1_pin = 23
coil_B_2_pin = 24

GPIO.setup(shutter_pin, GPIO.OUT)
GPIO.setup(coil_A_1_pin, GPIO.OUT)
GPIO.setup(coil_A_2_pin, GPIO.OUT)
GPIO.setup(coil_B_1_pin, GPIO.OUT)
GPIO.setup(coil_B_2_pin, GPIO.OUT)

def backwards(delay, steps, rounds):
	while rounds > 0:
		for i in range(0, steps):
			setStep(1, 0, 0, 1)
			time.sleep(delay)
			setStep(0, 1, 0, 1)
			time.sleep(delay)
			setStep(0, 1, 1, 0)
			time.sleep(delay)
			setStep(1, 0, 1, 0)
			time.sleep(delay)
			rounds = rounds - 1

def forwards(delay, steps, rounds):
	while rounds > 0:
		for i in range(0, steps):
			setStep(1, 0, 1, 0)
			time.sleep(delay)
			setStep(0, 1, 1, 0)
			time.sleep(delay)
			setStep(0, 1, 0, 1)
			time.sleep(delay)
			setStep(1, 0, 0, 1)
			time.sleep(delay)
			rounds = rounds - 1

def setStep(w1, w2, w3, w4):
	GPIO.output(coil_A_1_pin, w1)
	GPIO.output(coil_A_2_pin, w2)
	GPIO.output(coil_B_1_pin, w3)
	GPIO.output(coil_B_2_pin, w4)

while True:
	delay = 10
	steps = 10
	rounds = 650
	backwards(int(delay) / 1000.0, int(steps), int(rounds))
	time.sleep(3)
	forwards(int(delay) / 1000.0, int(steps), int(rounds))
	time.sleep(3)


