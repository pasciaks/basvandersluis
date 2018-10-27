# basvandersluis

Reference: https://www.youtube.com/watch?v=axuJAuYmwu0

Adding a switch to the Raspberry Pi GPIO pins without a pull-up or pull-down resistor - Code from Youtube post by author of the same name

# Here's the code from the video.  A comment mentioned how the text was too small to read in the video so I hereby provide this to help.



import RPi.GPIO as GPIO
from time import sleep

GPIO.setmode(GPIO.BOARD)
GPIO.setup(22, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(7, GPIO.OUT)

def buttonPressed(channel):
	if GPIO.input(22):
		print "released"
		GPIO.output(7,0)
	else:
		print "pressed"
		GPIO.output(7,1)
		
try:
	GPIO.add_event_detect(22, GPIO.BOTH, callback=buttonPressed)
	
	while True:
		sleep(0.1)
		
finally:
	GPIO.cleanup()
